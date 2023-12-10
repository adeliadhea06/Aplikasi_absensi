# Sistem Informasi Aplikasi Absensi Di SDIT Berbasis Web

Nama : Dhea Dwi Adelia

NIM : 312210116

Kelas : TI.22.A.1

Mata Kuliah : Rekayasa Perangkat Lunak

Dosen Pengampu : Wahyu Hadikristanto, S.Kom., M.Kom.

## Membuat Kode Program

### 1. login.php

    <?php
    session_start();
    include "koneksi.php";
    ?>
    
    <form action="" method="POST">
    	<table align="center" bgcolor="blue ice">
    		<tr>
    			<th colspan="2" height="40">LOGIN</th>
    		</tr>
    		<tr>
    			<td><input type="text" name="username" placeholder="Masukkan Username" size="25"> </td>
    		</tr>
    		<tr>
    			<td><input type="password" name="password" placeholder="Masukkan Password" size="25"></td>
    		</tr>
    		<tr>
    			<td><a href="registrasi.php"><input type="button" value="Saya Pengguna Baru" style="padding:5px; background-color: pink;"></a>
    			<input type="submit" value="Masuk" name="proseslog" style="padding:5px; background-color: pink;">
    			</td>
    		</tr>
    		</tr>
    	</table>
    </form>
    
    <?php
    if(isset($_POST['proseslog'])){
    	$sql =mysqli_query($koneksi,"select*from registrasi where username='$_POST[username]' and password='$_POST[password]'");
    
    	$cek=mysqli_num_rows($sql);
    	if ($cek > 0) {
    		$_SESSION['username']=$_POST['username'];
    
    		echo "<meta http-equiv=refresh content=0;URL='home.php'>";
    	} else{
    		echo "<p align=center><b>Username Dan Password Salah !</b></p>";
    		echo "<meta http-equiv=refresh content=2;URL:'login.php'>";
    	}
    }
    ?>


![image](https://github.com/adeliadhea06/Aplikasi_absensi/assets/115794875/47fed3c9-603b-43f5-8629-142f1a9a4281)

- Ketika login kita harus registrasi terlebih dahulu


### registrasi.php

    <!DOCTYPE html>
    <html>
    <head>
    	<title>Tambah Data</title>
    </head>
    <body>
    		<h1>Tambah Data</h1>
    		<form method="post" action="proses_simpan.php" enctype="multipart/form-data">
    			<table bgcolor="#FFC0CB" cellpadding="8">
    				<tr>
    				<td>Id</td>
    				<td><input type="text" name="id" placeholder="Masukkan id baru"></td>
    				<tr>
    				<td>Username</td>
    				<td><input type="text" name="username" placeholder="Masukkan username baru"></td>
    				</tr>
    				<tr>
    				<td>Password</td>
    				<td><input type="password" name="password" placeholder="Masukkan password baru"></td>
    				</tr>
    				<tr>
    				<td>Alamat</td>
    				<td><textarea name="alamat" placeholder="Masukkan alamat baru"></textarea></td>
    				</tr>
    				<tr>
    				<td>File</td>
    				<td><input type="file" name="file"></td>
    				</tr>
    		</table>
    
    			<input type="submit" value="Simpan">
    			<a href="login.php"><input type="button" value="Batal"></a>
    		</form>
    </body>
    </html>

![image](https://github.com/adeliadhea06/Aplikasi_absensi/assets/115794875/599450df-b5e7-4e6f-b36d-5447aa39acb4)


### proses_simpan.php

    <?php
    include "koneksi.php";
    $username=$_POST['username'];
    $password=$_POST['password'];
    $alamat=$_POST['alamat'];
    $file=$_FILES['file']['name'];
    $tmp=$_FILES['file']['tmp_name'];
    
    $fotobaru=date('dmYHis').$file;
    $path="berkas/".$fotobaru;
    if(move_uploaded_file($tmp, $path)){
    	$sql=$pdo->prepare("INSERT INTO registrasi(username, password, alamat, file) VALUES(:username,:password,:alamat,:file)");
    	$sql->bindParam(':username',$username);
    	$sql->bindParam(':password',$password);
    	$sql->bindParam(':alamat',$alamat);
    	$sql->bindParam(':file',$fotobaru);
    	$sql->execute();
    	if($sql){
    		header("location:login.php");
    	}else{
    		echo "maaf,terjadi kesalahan saat mencoba untuk menyimpan data ke database.";
    		echo "<br><a href='registrasi.php'>Kembali ke Form</a>";
    	}
    }else{
    	echo "Maaf,Gambar gagal untuk diupload.";
    	echo "<br><a href='registrasi.php'>Kembali Ke Form</a>";
    }
    ?>


### koneksi.php

Koneksi ini bertujuan untuk menghubungkan kode dengan __database__

    <?php
    
    $koneksi = mysqli_connect("localhost","root","","aplikasi_absensi");
    
    ?>


### session.php

    <?php
    session_start();
    if (!isset($_SESSION['username'])) {
    	header("location:login.php");
    }
    ?>


### home.php

    <?php
    include "session.php";
    include "koneksi.php";
    ?>
    
    <p align="center">
    
    <h1>Halo, Selamat Datang </h1><b></b></br>
    
    </p>
    <p align="right">
    	<a href="logout.php"><b> Logout</b></a>
    </p>

![Screenshot (545)](https://github.com/adeliadhea06/Aplikasi_absensi/assets/115794875/36359377-6fcb-483b-a091-9b3152b9c0af)


## Mohon Maaf Belum Lengkap
