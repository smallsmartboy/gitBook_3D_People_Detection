# A New Upsampling Method for Mobile LiDAR Data

> Ruisheng Wang, Jeff Bach, Jane Macfarlane

## 1.1. Related Work

There appears to be relatively little work in using co-registered intensity images to upsample range data, at least in comparison to pure image-based super-resolution, e.g.,[9, 10, 11]. 

```
[9] S. Farsiu, M. Robinson, M. Elad, and P. Milanfar. Fast and robust multiframe super resolution. IEEE Transactions on Image Processing, 13(10):1327–1344, Oct. 2004.
[10] S. Borman and R. L. Stevenson. Super-resolution from image sequences - a review. Proc. Midwest Symp. Circuits and Systems, 5, 1998.
[11] M. Irani and S. Peleg. Improving resolution by image registration. CVGIP: Graph. Models Image Process., 53(3):231--239, 1991.
```

초창기 연구 중 하나는 MRF를 이용한 방법이다. `One of the first attempts reported was basedon Markov Random Fields (MRFs) [1, 2, 3, 4]. `

- 가정사항 : 색이나 밝기 변화로 깊이 단절이 종종 발생한다. 문제는 깊이 단절은 색 채널에서는 보이지 않는다. `A common assumption here is that depth discontinuities in a scene often co-occur with color or brightness changes within the associated camera images. The problem occurs when a depth discontinuity is not visible in the color channel.`


```

[1] Luz A. Torres-Méndez and Gregory Dudek. RangeSynthesis for 3D Environment Modeling In 2002 IEEEWorkshop on Applications of Computer Vision, pp. 231--236, Orlando, FL, USA
[2] Luz Abril Torres-Méndez and Gregory Dudek.Reconstruction of 3D models from intensity images andpartial depth. Proceeding American Association forArtificial Intelligence (AAAI), 2004, pp. 476-481.
[3] J. Diebel and S. Thrun. An application of markov randomfields to range sensing. In Proceedings of Conference onNeural Information Processing Systems (NIPS),Cambridge, MA, 2005. MIT Press.
[4] Zhaoyin Jia, Yao-Jen Chang, Tzung-Han Lin, and TsuhanChen, "Dense 3D-Point Estimation Based on SurfaceFitting and Color Information," 2009 Western New YorkImage Processing Workshop, Henrietta, NY, USA, Sept.25, 2009.

```


Yang et al. [5] proposed an **iterative bilateral filtering method** for enhancing the resolution of range images. 

- The authors also compared their approach with MRF, showing that this method allows for sub-pixel accuracy. 

```
[5] Q. Yang, R. Yang, J. Davis, and D. Nist´er. Spatial-depth super resolution for range images. In CVPR, 2007.
```

Andreasson et al. [6] compared **five different interpolation schemes** with the MRF method [3] and summarized four different metrics for confidence measures of interpolated range data. (5개의 일반적 방식이 뭔지 참고 필요)
- 가정사항 : The assumption in their approach is similar to that of the MRF method which uses color similarity as an indication of depth similarity. 

```
[6] H. Andreasson, R. Triebel, and A. J. Lilienthal. Noniterative Vision-based Interpolation of 3D Laser Scans, volume 76 of Studies in Computational Intelligence, pages 83–90. Springer, Germany, Aug 14 2007.
```

In [8] points are projected onto segmented color images, and bilinear interpolation is used to compute the depth value of the grid samples that belong to the same region. 

```
[8] V. Garro, C. Dal Mutto, P. Zanuttigh, and G. M. Cortelazzo. A novel interpolation scheme for range data with side information. In Proc. of CVMP Conf., London, UK, November
```

[7] addresses the problem of upsampling range data in dynamic environments based on a Gaussian framework.

```
[7] Dolson, J.; Jongmin Baek; Plagemann, C.; Thrun, S.Upsampling range data in dynamic environments. IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2010.
```


슈퍼 리솔루션 방법 이요 `There is some work that does super resolution from depth data only. `
- 기본적이르 이 방식은 다른 뷰 포인트를 가지는 스트레오 카메라의 depth map을 이용한다. `Basically the goal is to enhance the resolution by using depth maps of a static scene that were acquired from slightly displaced viewpoints [12, 13].`


