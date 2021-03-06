# Cosimulation of AI Engine and Programmable Logic (HLS)
This example showcases a design containing both AI Engine blocks and Programmable Logic (HLS). We are using the *HLS Kernel* block to import an HLS kernel into Model Composer as a block. To connect the AI Engine blocks to the HLS kernel block, we use the *AIE to HLS* and *HLS to AIE* interface blocks if there is a data type mismatch, otherwise, we can connect the blocks directly. 

![](images/interface_blocks.PNG)

## Knowledge nuggets
:bulb: In Model Composer, you can cosimulate HLS kernels and AI Engine blocks.

:bulb: The HLS kernel code should have stream, or scalar or vector run-time parameter interfaces. 

:bulb: To import an HLS kernel, you should write a separate [header file](./src/hls_kernels.h) to declare function signatures and to specify hls::stream directions for HLS functions. In this special header file, the function signature is declared the same as in the HLS function definition, except that the input or output direction of a hls::stream data type is qualified using adf::dir::in<T> and adf::dir::out<T>, respectively.

:bulb: If the input and output data types of the AIE engine blocks match the data type of the interface to the HLS kernel block, there is no need to use the interface blocks. [aie_hls_std_complex.slx](./aie_hls_std_complex.slx) demonstrates an example. In essence, the interface blocks work as data type converters.

:warning: Note the need for *extern "C"* in the hls kernel function definition. 

![](images/screen_shot.png)

-----------

![](images/screen_shot_std_complex.png)

------------
Copyright 2020 Xilinx

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
