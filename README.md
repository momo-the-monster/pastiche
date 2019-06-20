pastiche
========

A PyTorch-based Python implementation of Neural Style Transfer [1].

<div align="center">
 <img src="https://github.com/dstein64/pastiche/blob/master/example/vangogh_starry_night.jpg?raw=true" height="256"/>
 <img src="https://github.com/dstein64/pastiche/blob/master/example/boston.jpg?raw=true" height="256"/>
 <br>
 <img src="https://github.com/dstein64/pastiche/blob/master/example/pastiche.jpg?raw=true" width="512"/>
</div>

Features
--------

- Support for saving intermediate images during optimization
- An option for preserving colors from the content image

Installation
------------

#### Requirements

- Python 3.5 or greater

#### Install

```sh
$ pip3 install pastiche
```

#### Update

```sh
$ pip3 install --upgrade pastiche
```

Usage
-----

The program is intended to be used from the command line.

There are various options, including but not limited to:
- Device (CPU versus GPU)
- Number of optimization iterations
- VGG layers to utilize
- Loss function term weights

For the full list of options and the corresponding documentation, see the source code or use `--help`.

```sh
$ pastiche --help
```

Usage
-----

The general command line usage is shown below.

```sh
$ pastiche CONTENT STYLE OUTPUT
```

`CONTENT` is the path to the content image, `STYLE` is the path to the style image, and `OUTPUT` is the path to save
the synthesized pastiche PNG file.

Use --help to access documentation for the additional options (e.g., --device for controlling whether to use a CPU
or GPU).

The style transfer image above was generated by applying the style from Vincent van Gogh's `The Starry Night` to
a photo I took in Boston in 2015. The high-resolution image was generated incrementally, with increasing resolution,
using the coarse-to-fine approach described in [2]. The commands are shown below. Depending on GPU memory availability,
the commands below may necessitate execution on a CPU (`--device cpu`).

```sh
$ pastiche \
    --num-steps 2000 \
    boston.jpg \
    vangogh_starry_night.jpg \
    pastiche0.png

$ pastiche \
    --size 1024 \
    --num-steps 1000 \
    --init --init pastiche0.png \
    boston.jpg \
    vangogh_starry_night.jpg \
    pastiche1.png

$ pastiche \
    --size 2048 \
    --num-steps 500 \
    --init --init pastiche1.png \
    boston.jpg \
    vangogh_starry_night.jpg \
    pastiche2.png

$ pastiche \
    --size 4096 \
    --num-steps 100 \
    --init --init pastiche2.png \
    boston.jpg \
    vangogh_starry_night.jpg \
    pastiche3.png

$ convert pastiche3.png pastiche.jpg  # requires ImageMagick
```

License
-------

The source code has an [MIT License](https://en.wikipedia.org/wiki/MIT_License).

See [LICENSE](https://github.com/dstein64/pastiche/blob/master/LICENSE).

References
----------

[1] Gatys, Leon A., Alexander S. Ecker, and Matthias Bethge. "A Neural Algorithm of Artistic Style."
ArXiv:1508.06576 [Cs, q-Bio], August 26, 2015. http://arxiv.org/abs/1508.06576.

[2] Gatys, Leon A., Alexander S. Ecker, Matthias Bethge, Aaron Hertzmann, and Eli Shechtman.
"Controlling Perceptual Factors in Neural Style Transfer." ArXiv:1611.07865 [Cs], November 23, 2016.
http://arxiv.org/abs/1611.07865.
