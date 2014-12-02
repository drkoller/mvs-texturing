#MVS-Texturing

Welcome to our project that textures 3D reconstructions from images.
This project focuses on 3D reconstructions generated using structure from
motion and multi-view stereo techniques, however, it is not limited to this
setting.

The algorithm was published in Sept. 2014 on the
*European Conference on Computer Vision*. Please refer to our project website
(http://www.gris.tu-darmstadt.de/projects/mvs-texturing)
for the paper and further information.


#Dependencies
The code and the build system have the following prerequisites:

- cmake (>= 2.8)
- git
- make
- gcc (>= 4.6.3) or a compatible compiler
- libpng, libjpg, libtiff


Furthermore the build system automatically downloads and compiles the following
dependencies (so there is nothing you need to do here):

- coldet
    http://sourceforge.net/projects/coldet/
- Eigen
    http://eigen.tuxfamily.org/
- Multi-View Environment
    http://www.gris.informatik.tu-darmstadt.de/projects/multiview-environment/

*The following is only downloaded if you use this software for research purposes and
thus provide the ```-DRESEARCH=ON``` flag (see compilation section below).*
- multi-label graph cut optimization
    http://vision.csd.uwo.ca/code/


#Compilation
1.  ```git clone https://github.com/nmoehrle/mvs-texturing.git```
2.  ```cd mvs-texturing```
3.  ```mkdir build && cd build```
4.  Generate make file
    * ```cmake ..```
    * **IMPORTANT**: For research purposes only you can use
    ```cmake -DRESEARCH=ON ..```
    instead. This downloads and links against Olga Veksler et al.'s multi-label
    graph cut optimization, which tends to find better optima and gives better
    texturing results. However, it is patented and can only be licensed for
    non-research purposes by the respective authors. For non-research purposes
    you have to stick to not using the RESEARCH flag. This will use Loopy Belief
    Propagation instead of Graph Cut Optimization. Also see the license section
    below for details.
5.  ```make``` (or ```make -j``` for parallel compilation)

If something goes wrong during compilation you should check the output of the
cmake step. CMake checks all dependencies and reports if anything is missing.

If you think that there is some problem with the build process on our side
please tell us.

If you are trying to compile this under windows (which should be possible but
we haven't checked it) and you feel like we should make minor fixes to support
this better, you can also tell us.


#Execution

As input our algorithm requires a triangulated 3D model and images that are
registered against this model. One way to obtain this is to:
*   import images, infer camera parameters and reconstruct depth maps
    using the [Multi-View Environment]
    (http://www.gris.informatik.tu-darmstadt.de/projects/multiview-environment/),
    and
*   fuse these depth maps into a combined 3D model using the
    [Floating Scale Surface Reconstruction]
    (http://www.gris.informatik.tu-darmstadt.de/projects/floating-scale-surface-recon/)
    algorithm.

A quick guide on how to use these applications can be found on our project [website](http://www.gris.informatik.tu-darmstadt.de/projects/mvs-texturing).

By starting the application without any parameters and you will get a
description of the expected file formats and optional parameters.


#License, Patents and Citing
Our software is licensed as described in the COPYING.txt file which is in the
same folder as this README.md file.

**IMPORTANT**: Using the ```-DRESEARCH=ON``` flag during compilation (see above) must
not be used if this software is used for other purposes than research. This
flag automatically downloads, compiles and links against multi-label graph cut
optimization which
> can be used only for research purposes. For commercial
  purposes, be aware that there is a US patent on the main algorithm itself.
  
*Cited from the multi-label graph cut optimization README file. See that file
for further information.*

If you use our texturing code for research purposes, please cite our paper:
```
@inproceedings{Waechter2014Texturing,
  title    = {Let There Be Color! --- {L}arge-Scale Texturing of {3D} Reconstructions},
  author   = {Waechter, Michael and Moehrle, Nils and Goesele, Michael},
  booktitle= {Proceedings of the European Conference on Computer Vision},
  year     = {2014},
  publisher= {Springer},
}
```


#Contact

If you have trouble compiling or using this software, if you found a bug or if
you have an important feature request, please contact us using the mail address
given in the paper or on the project web page:

http://www.gris.informatik.tu-darmstadt.de/projects/mvs-texturing
