# tutorial_gazebo-simple-model
This tutorial shows how to create a simple single body model and how to spawn it in the [Gazebo simulator](http://gazebosim.org/). 

[![Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/from-referrer)

## Prerequisites

For this tutorial, you just need to be aware of:
- What the [Gazebo simulator](http://gazebosim.org/) is
- Optionally run [CMake](https://cmake.org/)

## You will see how to:
- How to create a Gazebo model from a [mesh](https://en.wikipedia.org/wiki/Polygon_mesh) of a given object.
- How to install a Gazebo model in way that it can be found automatically by Gazebo.

## Related docs 
- [Gazebo : Tutorial : Quick Start](http://gazebosim.org/tutorials?tut=quick_start)
- [Gazebo : Tutorial : Gazebo Components](http://gazebosim.org/tutorials?tut=components)
- [Gazebo : Tutorial : Make a Model](http://gazebosim.org/tutorials?tut=build_model)
- [Gazebo : Tutorial : Building a World](http://gazebosim.org/tutorials?tut=build_world)
- [Specifying pose in SDFormat](http://sdformat.org/tutorials?tut=specify_pose)

## Build and Install the code
Follow these steps to build and properly install your module: 
```
$ cd tutorial_gazebo-simple-model
$ mkdir build; cd build
$ cmake ../
# make is not necessary as this project does not compile anything
$ make install
```
the `make install` will install your model and related files in the icub contrib folder which is already setup on your machine. 

## Contents
The repo contains the following files: 
* [`CMakeLists.txt`](CMakeLists.txt) : The file that describes where the files contained in the are installed by `make install` . 
* [`gazebo/models/simple_object/model.config`](gazebo/models/simple_object/model.config) : A file containing metadata related to the `simple_object` model. 
* [`gazebo/models/simple_object/simple_object.sdf`](gazebo/models/simple_object/simple_object.sdf) : A [sdf](http://sdformat.org/) file describing the model of the `simple_object`.
* [`gazebo/models/simple_object/simple_object.stl`](gazebo/models/simple_object/simple_object.stl) : A [stl](https://en.wikipedia.org/wiki/STL_(file_format)) file describing the shape of the `simple_object`.
* [`gazebo/worlds/simple_object_world.sdf`](gazebo/models/simple_object/simple_object.sdf) : A [sdf](http://sdformat.org/) file describing the world that contains the `simple_object` model. 

To understand the role of each file, please open the files and see the internal comments, except for the `.stl` file that is 
a binary format and not a textual one.  

## Use the installed models 

### Spawn from GUI
After you installed the repository, open Gazebo by running the `gazebo` command in the terminal: 
~~~
gazebo
~~~
In the list of models in the panel on the left, you can find the `simple_object` model, drag it in the GUI to spawn an instance of it in the simulation.

### Spawn from a world file 
You can also run directly a simulation from a world file that contains all the models that needs to be simulated, 
by running gazebo from the terminal followed by the name of the world file: 
~~~
gazebo simple_object_world.sdf
~~~

### Spawn from a world file in yarpmanager
To launch a simulation from the yarpmanager, it is usually convenient to separate the launch 
of the physics simulation program (`gzserver`) and the GUI client (`gzclient`). In this case, 
you need to pass the name of the world to the `gzserver` command:
~~~
gzserver simple_object_world.sdf
~~~
while the `gzclient` can be run directly: 
~~~
gzclient
~~~

### How Gazebo find models and world files 
In the context of this tutorial, you don't need to worry about how Gazebo is able to find the models 
and the world installed by the `make install`. 
However, in general, to be found models directories should be installed in the directories listed in the 
`GAZEBO_MODEL_PATH` enviroment variable and world files in the directories listed in `GAZEBO_RESOURCE_PATH` . 
For more details on how models and world files are found in general in Gazebo, please check the [Gazebo : Tutorial : Gazebo Components](http://gazebosim.org/tutorials?tut=components).

## How to add a new model
If you want to add a new simple single body model to this tutorial, you can proceed as follows: 
* Copy the content of the `gazebo/models/simple_object` directory in a new directory, for example `gazebo/models/new_simple_object`
* Update the `gazebo/models/new_simple_object/model.config` `//model/name` content from `simple_object`
  to `new_simple_object`, and `//model/sdf` from `simple_object.sdf` to `new_simple_object.sdf`.
* Rename the `gazebo/models/new_simple_object/simple_object.sdf` to `gazebo/models/new_simple_object/new_simple_object.sdf`.
  In that file, update the `//sdf/model@name` attribute from `simple_object` to `new_simple_object`. If necessary,
  update the inertia values, but if the `//sdf/model/static` value remains set to false, you can just ignore the inertia parameters. 
* Get a STL mesh for your object, and save it as `gazebo/models/new_simple_object/new_simple_object.stl`, and update the `uri` values 
  in the `gazebo/models/new_simple_object/mew_simple_object.sdf` to point to the new mesh files. 
* If necessary, add a new world that uses the new model in `gazebo/worlds`.
