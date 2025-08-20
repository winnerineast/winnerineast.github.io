Paper – [https://arxiv.org/abs/2508.11386](https://t.co/E1F7XY1g8R)

Paper Title: "Retrieval-augmented reasoning with lean language models"

A small Qwen2.5 model is fine-tuned to think over retrieved documents, so a single lean setup can answer domain questions on resource-constrained local hardware.

Using summarised NHS pages, retrieval hits the right condition among top‑5 in 76% of queries, and the fine‑tuned model predicts the exact condition correctly 56% of the time, close to larger frontier models. 

The whole pipeline is built for private deployments, so teams can run it without sending data to external APIs.

🔒 The problem they tackle

Many teams cannot ship prompts or data outside their network, especially in health and government, so cloud LLM endpoints are off the table. 

They aim for a single lean model that can read retrieved evidence and reason over it, all running locally, so answers stay grounded and private. 

The target setting is messy queries over a closed corpus, where retrieval constrains facts and the reasoning step interprets symptoms and next actions.

🧩 The pipeline in this paper.

The system indexes a corpus, retrieves the most relevant pieces for each query, then generates an answer that reasons over those pieces. 

They use a classic retriever plus generator design, with retrieval first then reasoning, which fits decision tasks better than free‑form answering. 

The chat flow lets a conversational agent decide when to call retrieval, then passes the retrieved context to the reasoning model to produce the answer.

<img width="789" height="826" alt="Image" src="https://github.com/user-attachments/assets/d0c0b06a-d1bf-429e-9ca2-82b6e0b58be1" />

The retriever at work

Documents are split into overlapping chunks and embedded with a sentence transformer, then stored in a vector database for fast similarity search. 

They use sentence-transformers all‑mpnet‑base‑v2, which maps text into a 768‑dimensional space with a max sequence of 384 tokens, and a Chroma store with L2 similarity. 

If any chunk from a document makes the top‑k, the pipeline feeds the full original document to the LLM, so the model sees full context around the hit.

<img width="672" height="288" alt="Image" src="https://github.com/user-attachments/assets/f8f16b8d-0535-4757-b932-edea32e736af" />

Below image shows the whole training loop for their lean, retrieval-augmented reasoning setup. 

It starts with a private knowledge base of about 1,000 NHS condition pages. GPT-4o generates about 2,000 synthetic patient queries from those pages, so they have realistic questions tied to known answers. 

For each query, a retriever pulls the top 5 likely documents. DeepSeek-R1 reads those documents and the query, then produces a final label plus a step-by-step reasoning trace. That bundle becomes one training example. 

They then fine-tune Qwen-32B-Instruct on this data and distill it into a smaller t0-1 reasoning model. The result is a compact model that learns to reason over retrieved evidence from the approved corpus, so it can run locally and stay grounded.

<img width="720" height="426" alt="Image" src="https://github.com/user-attachments/assets/ae38a29c-09af-4eb5-9029-3e97e2d0f868" />

 How the data was built

They generate realistic patient queries plus demographics from the NHS Conditions pages using GPT‑4o, covering basic, hypochondriac, and downplay styles. 

They create 1,000 queries for evaluation and 2,000 for training, checking there is no overlap in condition plus disposition pairs between the 2 sets. 

For each training query they retrieve k=5 candidate condition pages, then ask DeepSeek‑R1 to produce a reasoning trace and a final label, which becomes supervision.
<img width="679" height="376" alt="Image" src="https://github.com/user-attachments/assets/2bbe1de5-e30a-4202-b0aa-9c937b58d2a9" />

Keeping context short

Full documents made traces extremely long, averaging 74,641 tokens when retrieving 5 documents, which would blow up fine‑tune compute. 

They summarise every document up front by 85%, then build traces from summaries, dropping the average trace length to 7,544 tokens, while keeping retrieval quality intact. 

Query‑aware summarisation was considered, but it would add an extra LLM call per query, so they stick to static summaries for speed.
<img width="705" height="427" alt="Image" src="https://github.com/user-attachments/assets/b3327f4d-e1dd-46f0-a18f-336d046047dc" />

Fine‑tuning and compute

They fine‑tune Qwen2.5‑Instruct models from 1.5B to 32B parameters on next‑token prediction of the traces, using 5 epochs, cosine LR at 1e‑5, bf16, and FSDP sharding. 

The long‑context setup uses block size 32,768, gradient checkpointing, and Adam with weight decay 1e‑4, beta1 0.9, beta2 0.95. 

The main 32B run uses 16 A100 80GB GPUs, and the whole study spans Azure plus 2 UK HPC clusters, totalling roughly 3,700 GPU‑hours.

<img width="653" height="621" alt="Image" src="https://github.com/user-attachments/assets/fe4dd20e-3a64-431e-ae23-199e3fd7109e" />

What retrieval recovered

On the 989 summarised pages, retrieval finds the correct condition in the top‑5 for 76% of queries, and top‑30 for 93%, which sets the ceiling for end‑to‑end accuracy when k=5. 

Summaries actually retrieve better than full chunks at the same k, because they remove boilerplate and keep the decision cues. 

They choose k=5 as a practical trade‑off, keeping prompts small enough for stable training and easier inspection in the UI.

