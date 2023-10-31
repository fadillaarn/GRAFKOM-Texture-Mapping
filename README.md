## Assignment Texture Mapping

| Nama | NRP |
|:----:|:---:|
| Fadilla Rizky Nurhidayah | 5025211110 |

## Function Draw
```   
    drawSquare(textureObjects[0]);  // front face
    mat4.rotateY(modelview, modelview, Math.PI/2);
    drawSquare(textureObjects[1]);  // right face
    mat4.rotateY(modelview, modelview, Math.PI/2);
    drawSquare(textureObjects[2]);  // back face
    mat4.rotateY(modelview, modelview, Math.PI/2);
    drawSquare(textureObjects[3]);  // left face
    mat4.rotateY(modelview, modelview, Math.PI / 2);
    mat4.rotateX(modelview, modelview, -Math.PI/2);
    drawSquare(textureObjects[4]);  // top face
    mat4.rotateX(modelview, modelview, Math.PI);
    drawSquare(textureObjects[5]);  // bottom face
}
```
## Function initGL
```
let loadedImages = 0; // To keep track of loaded images
    for (let i = 0; i < 6; i++) {
        img[i] = new Image();
        img[i].onload = function (index) { // Use a closure to capture the value of i
        return function () {
            textureObjects[index] = gl.createTexture();
            gl.bindTexture(gl.TEXTURE_2D, textureObjects[index]);
            gl.texImage2D(
                gl.TEXTURE_2D,
                0,
                gl.RGBA,
                gl.RGBA,
                gl.UNSIGNED_BYTE,
                img[index]
            );
            gl.generateMipmap(gl.TEXTURE_2D);
            loadedImages++;

            if (loadedImages === 6) {
                // All images are loaded, so you can call the draw function here
                draw();
            }
        };
    }(i); // Pass the current value of i to the closure

    img[i].src = textureURLs[i];
    }
```
