## caffe-tutorial
#### Slice layer 

Decompose `bottom` into several `tops` (Split layer copies `bottoms`, output to `tops`).
```
layer {
  name: "slice"
  type: "Slice"
  bottom: "input"
  top: "output1"
  top: "output2"
  top: "output3"
  top: "output4"
  slice_param {
    axis: 1
    slice_point: 1
    slice_point: 3
    slice_point: 4
  }
}
```
given the dimention of bottom: `N*5*H*W`, the dimentions of output tops are `N*1*H*W N*2*H*W N*1*H*W N*1*H*W`, respectively.
`axis` indicates the target axis;     
`slice_point` indicates indexes in the selected dimension (the number of indices must be equal to the number of top blobs minus one).

#### Silence layer
```
layer {
  name: "silence_name"
  type: "Silence"
  bottom: "silence_layer"
  phase: "TRAIN"
}
```

#### Crop layer
`layer_to_crop`: [4,16,256,256]

`layer_refer`: [4,10,128,128]

`layer_after_crop`: [4,6,128,128]

```
layer {
  name: "layer_after_crop"
  type: "Crop"
  bottom: "layer_to_crop"
  bottom: "layer_refer"
  top: "layer_after_crop"
  crop_param {
    axis: 1
    offset: 6
    offset: 128
    offset:128
  }
}
```

