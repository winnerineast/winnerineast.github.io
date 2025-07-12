https://deepbrainai-research.github.io/float/
### Generative Motion Latent Flow Matching for Audio-driven Talking Portrait

[Taekyung Ki1](https://taekyungki.github.io/) [Dongchan Min2](https://kevinmin95.github.io/) [Gyeongsu Chae1](https://www.aistudios.com/ko/home)

1DeepBrain AI Inc. 2Graduate School of AI, KAIST

ArXiv 2024

[Paper (Soon)](https://deepbrainai-research.github.io/float/) [Video (Soon)](https://deepbrainai-research.github.io/float/) [Code (Soon)](https://deepbrainai-research.github.io/float/)

## Abstract

![](https://deepbrainai-research.github.io/float/src/img/float-abstract.png)  

With the rapid advancement of diffusion-based generative models, portrait image animation has achieved remarkable results. However, it still faces challenges in temporally consistent video generation and fast sampling due to its iterative sampling nature. This paper presents FLOAT, an audio-driven talking portrait video generation method based on flow matching generative model. We shift the generative modeling from the pixel-based latent space to a learned motion latent space, enabling efficient design of temporally consistent motion. To achieve this, we introduce a transformer-based vector field predictor with a simple yet effective frame-wise conditioning mechanism. Additionally, our method supports speech-driven emotion enhancement, enabling a natural incorporation of expressive motions. Extensive experiments demonstrate that our method outperforms state-of-the-art audio-driven talking portrait methods in terms of visual quality, motion fidelity, and efficiency.

TL;DR: FLOAT is a flow matching based audio-driven talking portrait video generation method, which can enhance the speech-driven emotional motion.

## Method Overview

![Responsive image](https://deepbrainai-research.github.io/float/src/img/overview.png)

Audio-driven talking portrait aims to synthesize talking portrait videos using a single source portrait image and driving audio. FLOAT is built upon a motion latent auto-encoder that encodes the given portrait image into an (identity-motion) latent representation. We generates audio-conditioned talking portrait motion latents through the flow matching (with optimal transport trajectories). To enhace the naturalness of generated talking motion, we incorporate the speech-driven emotion labels (😀), providing a natural approach of emotion-aware talking portrait motion generation.

## Results

  

#### Results with Out-of-distribution Datas

FLOAT can generate realistic talking portrait videos using OOD portrait images and audio.

  

  

  
  

#### Emotion Redirection

Since FLOAT is trained with speech-driven emotion labels, it can re-direct the emotion of the talking portrait during the inference phase. Specifically, we can manipulate the predicted speech-driven emotion label with a simple one-hot emotion label, which can be further refined through classifier-free vector fields. This enables users to refine emotion even when the driving speech conveys ambiguious or mixed emotions.

  

  
  

#### Comparison with State-of-the-art Methods

We compare with state-of-the-art non-diffusion-based methods and diffusion-based methods. For non-diffusion-based methods, we choose SadTalker and EDTalk. For diffusion-based methods, we choose AniTalker, Hallo, and EchoMimic.

[Previous](https://deepbrainai-research.github.io/float/#carouselExampleControls)[Next](https://deepbrainai-research.github.io/float/#carouselExampleControls)

  
  

#### Ablation Studies on Frame-wise AdaLN and Flow Matching

We conduct ablation studies on frame-wise AdaLN (and gating) and flow matching. For frame-wise AdaLN (and gating), we compare it with cross-attention mechanism, which is widely used in conditional generation. For flow matching, we compare it with two types of diffusion models (ϵϵ-prediction and x0x0-prediction). We observe that frame-wise AdaLN (and gating) can generate more diverse head motions than cross-attention. We also observe that flow mathcing can generate more temporally consistent videos with accurate lip-synchronization than diffusion models.

[Previous](https://deepbrainai-research.github.io/float/#carouselExampleControls1)[Next](https://deepbrainai-research.github.io/float/#carouselExampleControls1)

  
  

#### Different Number of Function Evaluations (NFEs)

The small number of function evaluations (NFEs) affects temporal consistency. This is because we generate the motion latents, not the content itself. FLOAT is capable of generating reasonable video results with approximately 10 NFEs.

[Previous](https://deepbrainai-research.github.io/float/#carouselExampleControls2)[Next](https://deepbrainai-research.github.io/float/#carouselExampleControls2)

  
  

#### Emotion Guidance Scales

We can control the intensity of the emotion by adjusting the emotion guidance scale. Note that the predicted speech-driven emotion label is **Disgust** with a 99.99% probability.

  
  

#### Additional Driving Conditions

We also investigate another types of driving conditions, such as 3DMM head pose parameters, to improve the controllability and naturalness. Here, 3DPose, S2E, and I2E are 3DMM head pose parameters, Speech-to-emotion label, and Image-to-emotion label, resepctively.

  

  
  

#### Ablation Study on Facial Component Perceptual Loss in Phase 1

The proposed facial component perceptual loss for the motion latent auto-encoder significantly improves visual quality (e.g., teeth and eyes), as well as fine-grained motion (e.g., eyeball movement and lip motion).

  

## Citation

If you want to cite our work, please use:

          TBA
          
      

## Acknowledgement

The source images and audio are collected from the internet and other baselines, such as SadTalker, EMO, VASA-1, Hallo, LivePortrait, Loopy, and others. We appreciate their valuable contributions to this field. This project page is based on the project page of [RegNeRF](https://m-niemeyer.github.io/regnerf). You can easily use it from [the github repository](https://github.com/m-niemeyer/regnerf).