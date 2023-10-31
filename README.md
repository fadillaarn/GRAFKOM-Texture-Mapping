## Assignment Texture Mapping

| Nama | NRP |
|:----:|:---:|
| Fadilla Rizky Nurhidayah | 5025211110 |

## Penjelasan

### Perubahan pada Function initGL
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

Kode di atas digunakan untuk memuat gambar-gambar yang akan digunakan sebagai tekstur dalam WebGL. Kode ini menggunakan perulangan untuk menginisialisasi dan memuat gambar ke dalam array "img". Saat setiap gambar selesai dimuat, sebuah fungsi handler "onload" dipanggil. Dalam fungsi handler ini, objek tekstur WebGL diciptakan dan dihubungkan dengan gambar yang sesuai. Gambar tersebut kemudian dijadikan tekstur dalam WebGL, dan setiap kali gambar selesai dimuat, variabel "loadedImages" akan ditingkatkan. Ketika semua gambar telah dimuat (sejumlah 6 gambar), maka fungsi "draw()" akan dipanggil, memungkinkan penggambaran objek 3D menggunakan tekstur yang telah dimuat sebelumnya. Ini adalah cara yang efisien untuk mengelola pemrosesan asinkron gambar sebelum menggambar objek dalam WebGL.

## Perubahan pada Function Draw
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
Kode di atas adalah bagian dari proses penggambaran objek kubus dalam  WebGL. Setiap baris menyatakan penggambaran satu sisi kubus dengan tekstur yang sesuai. Setelah menggambar sisi depan, sisi kanan, sisi belakang, dan sisi kiri, matriks "modelview" diputar 90 derajat sekitar sumbu Y, sehingga gambaran objek 3D bisa beralih ke sisi atas. Selanjutnya, matriks "modelview" juga diputar 90 derajat sekitar sumbu X untuk menggambar sisi atas dan bawah kubus. Ini adalah bagian dari langkah-langkah untuk menggambar seluruh kubus dalam berbagai orientasi dengan tekstur yang sesuai pada masing-masing sisi.

## Output 

### Left and Right Face
<img width="1680" alt="Screenshot 2023-10-31 at 12 03 13" src="https://github.com/fadillaarn/GRAFKOM-Texture-Mapping/assets/91003946/bd8a27b7-0e74-4657-8a52-0d39949a2281">

### Bottom Face
<img width="1680" alt="Screenshot 2023-10-31 at 12 03 23" src="https://github.com/fadillaarn/GRAFKOM-Texture-Mapping/assets/91003946/c960cdd2-b9c3-42b9-bf82-4b78233c3947">

### Top Face
![Screenshot 2023-10-31 at 12 03 37](https://github.com/fadillaarn/GRAFKOM-Texture-Mapping/assets/91003946/ff42b699-50f4-4b0d-bb18-c68be7f6a06b)
