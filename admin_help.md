<?php
$target_dir = "uploads/";
$target_file = $target_dir . basename($_FILES["fileToUpload"]["name"]);
$uploadOk = 1;
$imageFileType = strtolower(pathinfo($target_file,PATHINFO_EXTENSION));

// Check if image file is a actual image or fake image
if(isset($_POST["submit"])) {
  $check = getimagesize($_FILES["fileToUpload"]["tmp_name"]);
  if($check !== false) {
    echo "File is an image - " . $check["mime"] . ".";
    $uploadOk = 1;
  } else {
    echo "File is not an image.";
    $uploadOk = 0;
  }
}

// Check if file already exists
if (file_exists($target_file)) {
  echo "Sorry, file already exists.";
  $uploadOk = 0;
}

// Check file size
if ($_FILES["fileToUpload"]["size"] > 500000) {
  echo "Sorry, your file is too large.";
  $uploadOk = 0;
}

// Allow certain file formats
if($imageFileType != "jpg" && $imageFileType != "png" && $imageFileType != "jpeg"
&& $imageFileType != "gif" ) {
  echo "Sorry, only JPG, JPEG, PNG & GIF files are allowed.";
  $uploadOk = 0;
}

// Check if $uploadOk is set to 0 by an error
if ($uploadOk == 0) {
  echo "Sorry, your file was not uploaded.";
// if everything is ok, try to upload file
} else {
  if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], $target_file)) {
    echo "The file ". htmlspecialchars( basename( $_FILES["fileToUpload"]["name"])). " has been uploaded.";
  } else {
    echo "Sorry, there was an error uploading your file.";
  }
}
?>


<?php

// Get reference to uploaded image
$image_file = $_FILES["image"];

// Exit if no file uploaded
if (!isset($image_file)) {
    die('No file uploaded.');
}

// Exit if image file is zero bytes
if (filesize($image_file["tmp_name"]) <= 0) {
    die('Uploaded file has no contents.');
}

// Exit if is not a valid image file
$image_type = exif_imagetype($image_file["tmp_name"]);
if (!$image_type) {
    die('Uploaded file is not an image.');
}

// Get file extension based on file type, to prepend a dot we pass true as the second parameter
$image_extension = image_type_to_extension($image_type, true);

// Create a unique image name
$image_name = bin2hex(random_bytes(16)) . $image_extension;

// Move the temp image file to the images directory
move_uploaded_file(
    // Temp image location
    $image_file["tmp_name"],

    // New image location
    __DIR__ . "/images/" . $image_name
);


----------------------------

<?php

header('Content-Type: text/plain; charset=utf-8');

try {
    
    // Undefined | Multiple Files | $_FILES Corruption Attack
    // If this request falls under any of them, treat it invalid.
    if (
        !isset($_FILES['upfile']['error']) ||
        is_array($_FILES['upfile']['error'])
    ) {
        throw new RuntimeException('Invalid parameters.');
    }

    // Check $_FILES['upfile']['error'] value.
    switch ($_FILES['upfile']['error']) {
        case UPLOAD_ERR_OK:
            break;
        case UPLOAD_ERR_NO_FILE:
            throw new RuntimeException('No file sent.');
        case UPLOAD_ERR_INI_SIZE:
        case UPLOAD_ERR_FORM_SIZE:
            throw new RuntimeException('Exceeded filesize limit.');
        default:
            throw new RuntimeException('Unknown errors.');
    }

    // You should also check filesize here. 
    if ($_FILES['upfile']['size'] > 1000000) {
        throw new RuntimeException('Exceeded filesize limit.');
    }

    // DO NOT TRUST $_FILES['upfile']['mime'] VALUE !!
    // Check MIME Type by yourself.
    $finfo = new finfo(FILEINFO_MIME_TYPE);
    if (false === $ext = array_search(
        $finfo->file($_FILES['upfile']['tmp_name']),
        array(
            'jpg' => 'image/jpeg',
            'png' => 'image/png',
            'gif' => 'image/gif',
        ),
        true
    )) {
        throw new RuntimeException('Invalid file format.');
    }

    // You should name it uniquely.
    // DO NOT USE $_FILES['upfile']['name'] WITHOUT ANY VALIDATION !!
    // On this example, obtain safe unique name from its binary data.
    if (!move_uploaded_file(
        $_FILES['upfile']['tmp_name'],
        sprintf('./uploads/%s.%s',
            sha1_file($_FILES['upfile']['tmp_name']),
            $ext
        )
    )) {
        throw new RuntimeException('Failed to move uploaded file.');
    }

    echo 'File is uploaded successfully.';

} catch (RuntimeException $e) {

    echo $e->getMessage();

}

?>



<?php

if ($type == 'application/x-macbinary') {

    if (strlen($content) < 128) die('File too small');

    $length = 0;

    for ($i=83; $i<=86; $i++) {

        $length = ($length * 256) + ord(substr($content,$i,1));

          }

    $content = substr($content,128,$length);

}

?>


----------------------------------
<!DOCTYPE html>

<html>

<head>

    <title>Image Upload in PHP</title>

    <! link the css file to style the form >

    <link rel="stylesheet" type="text/css" href="style.css" />

</head>

<body>

    <div id="wrapper">

        <! specify the encoding type of the form using the 

                enctype attribute >

        <form method="POST" action="" enctype="multipart/form-data">        

            <input type="file" name="choosefile" value="" />

            <div>

                <button type="submit" name="uploadfile">

                UPLOAD

                </button>

            </div>

        </form>

    </div>

</body>

</html>

The following CSS code is for giving a basic styling to the HTML form.

#wrapper{

    width: 50%;

    margin: 20px auto;

    border: 2px solid #dad7d7;

}

form{

    width: 50%;

    margin: 20px auto;

}

form div{

    margin-top: 5px;

}

img{

    float: left;

    margin: 5px;

    width: 280px;

    height: 120px;

}

#img_div{

    width: 70%;

    padding: 5px;

    margin: 15px auto;

    border: 1px solid #dad7d7;

}

#img_div:after{

    content: "";

    display: block;

    clear: both;

}


Image Upload in PHP: A Step-by-Step Explanation
By Ravikiran A S
Last updated on Feb 17, 202392505
Interpreting Image Upload in PHP
Table of Contents

Program to Achieve the TaskProgram ExplanationPHP Methods Used in the ProgramFinal Code Combining the PHP, CSS, and HTMLSteps to Exceed the Size of Image UploadView More
PHP is widely used in developing server-side applications. On a dynamic website, uploading files to keep it updated is a routine. And PHP efficiently handles this process. You can use PHP to handle the uploading of multiple files to the server and display them on a dynamic website. 

PHP is used with almost all popular database software. MySQL is one of the most popular databases used in PHP applications. There are many other databases such as PostgreSQL, SYBASE, Oracle Database, and so on that can easily connect with your PHP applications. 

An image can be uploaded and displayed on your PHP website in multiple ways. The most common method of achieving this is by uploading the image into the server’s directory and updating its name in the database. This method is efficient because in this case, the image won’t take any space inside the database, and this will also make your webpage load faster. Another way is by inserting the image into the database directly, instead of uploading it into the server. This method is not recommended because the images take up a lot of space in the database, thereby increasing its size. This will also slow down the loading of your web pages. 

Basics to Advanced - Learn It All!

Caltech PGP Full Stack DevelopmentEXPLORE PROGRAMBasics to Advanced - Learn It All!
In this article, you will look into an efficient method to achieve image upload in PHP, by uploading the image file into a server directory and simply inserting the file name in a database. The file name is used to retrieve the desired file later on, and display it on your website. You will use a MySQL database to demonstrate image upload in PHP.

The following steps need to be followed to upload an image and display it on a website using PHP:

Create a form using HTML for uploading the image files.
Connect with the database to insert the image file.
Program to Achieve the Task

Step 1: Create a Form Using HTML for Uploading the Image Files.

The following HTML code will create a simple form on your website, with a “choose file” option and a button to upload the chosen file.

<!DOCTYPE html>

<html>

<head>

    <title>Image Upload in PHP</title>

    <! link the css file to style the form >

    <link rel="stylesheet" type="text/css" href="style.css" />

</head>

<body>

    <div id="wrapper">

        <! specify the encoding type of the form using the 

                enctype attribute >

        <form method="POST" action="" enctype="multipart/form-data">        

            <input type="file" name="choosefile" value="" />

            <div>

                <button type="submit" name="uploadfile">

                UPLOAD

                </button>

            </div>

        </form>

    </div>

</body>

</html>

The following CSS code is for giving a basic styling to the HTML form.

#wrapper{

    width: 50%;

    margin: 20px auto;

    border: 2px solid #dad7d7;

}

form{

    width: 50%;

    margin: 20px auto;

}

form div{

    margin-top: 5px;

}

img{

    float: left;

    margin: 5px;

    width: 280px;

    height: 120px;

}

#img_div{

    width: 70%;

    padding: 5px;

    margin: 15px auto;

    border: 1px solid #dad7d7;

}

#img_div:after{

    content: "";

    display: block;

    clear: both;

}

Learn from the Best in the Industry!

Caltech PGP Full Stack DevelopmentEXPLORE PROGRAMLearn from the Best in the Industry!
Step 2: Connect With the Database to Insert the Image File.

The following PHP code will connect the database to insert the submitted data into the database.

<?php

error_reporting(0);

?>

<?php

$msg = ""; 

// check if the user has clicked the button "UPLOAD" 

if (isset($_POST['uploadfile'])) {

    $filename = $_FILES["choosefile"]["name"];

    $tempname = $_FILES["choosefile"]["tmp_name"];  

        $folder = "image/".$filename;   

    // connect with the database

    $db = mysqli_connect("localhost", "root", "", "Image_Upload"); 

        // query to insert the submitted data

        $sql = "INSERT INTO image (filename) VALUES ('$filename')";

        // function to execute above query

        mysqli_query($db, $sql);       

        // Add the image to the "image" folder"

        if (move_uploaded_file($tempname, $folder)) {

            $msg = "Image uploaded successfully";

        }else{

            $msg = "Failed to upload image";

    }

}

$result = mysqli_query($db, "SELECT * FROM image");

?>

-----------------------------
<?php

error_reporting(0);

?>

<?php

$msg = "";

// check if the user has clicked the button "UPLOAD" 

if (isset($_POST['uploadfile'])) {

    $filename = $_FILES["choosefile"]["name"];

    $tempname = $_FILES["choosefile"]["tmp_name"];  

        $folder = "image/".$filename;

      // connect with the database

    $db = mysqli_connect("localhost", "root", "", "Image_upload");

        // query to insert the submitted data

        $sql = "INSERT INTO image (filename) VALUES ('$filename')";

     // function to execute above query

        mysqli_query($db, $sql);       

        // Add the image to the "image" folder"

        if (move_uploaded_file($tempname, $folder)) {

            $msg = "Image uploaded successfully";

        }else{

            $msg = "Failed to upload image";

    }

}

$result = mysqli_query($db, "SELECT * FROM image");

?> 

<!DOCTYPE html>

<html> 

<!DOCTYPE html>

<html>

 <head>

    <title>Image Upload in PHP</title>

    <! link the css file to style the form >

    <link rel="stylesheet" type="text/css" href="style.css" />

  <style type="text/css">

        #wrapper{

            width: 50%;

            margin: 20px auto;

            border: 2px solid #dad7d7;

        }

        form{

            width: 50%;

            margin: 20px auto;

        }

        form div{

            margin-top: 5px;

        }

        img{

            float: left;

            margin: 5px;

            width: 280px;

            height: 120px;

        }

        #img_div{

            width: 70%;

            padding: 5px;

            margin: 15px auto;

            border: 1px solid #dad7d7;

        }

        #img_div:after{

            content: "";

            display: block;

            clear: both;

        }

    </style>

</head>

 <body>

    <div id="wrapper">

         <! specify the encoding type of the form using the 

                enctype attribute >

         <form method="POST" action="" enctype="multipart/form-data">

                  <input type="file" name="choosefile" value="" />

            <div>

                <button type="submit" name="uploadfile">WAMP or XAMPP server

                UPLOAD

                </button>

            </div>

        </form>

    </div>

</body>

</html>

------------------------------------

composer create-project laravel/laravel example-app

php artisan make:controller ImageUploadController

<?php
  
namespace App\Http\Controllers;
  
use Illuminate\Http\Request;
  
class ImageUploadController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        return view('imageUpload');
    }
      
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        $request->validate([
            'image' => 'required|image|mimes:jpeg,png,jpg,gif,svg|max:2048',
        ]);
      
        $imageName = time().'.'.$request->image->extension();  
       
        $request->image->move(public_path('images'), $imageName);
    
        /* 
            Write Code Here for
            Store $imageName name in DATABASE from HERE 
        */
      
        return back()
            ->with('success','You have successfully upload image.')
            ->with('image',$imageName); 
    }
}

$request->image->storeAs('images', $imageName);
// storage/app/images/file.png

$request->image->move(public_path('images'), $imageName);
// public/images/file.png

$request->image->storeAs('images', $imageName, 's3');


<!--?php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\ImageUploadController;
/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/
Route::get('upload-image', [ ImageUploadController::class, 'index' ]);
Route::post('upload-image', [ ImageUploadController::class, 'store' ])--->name('image.store');


<!DOCTYPE html>
<html>
<head>
    <title>How to Upload Image in Laravel 9? - LaravelTuts.com</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
<div class="container">
    <div class="panel panel-primary">
        <div class="panel-heading mt-5 text-center">
            <h2>How to Upload Image in Laravel 9? - LaravelTuts.com</h2>
        </div>
 
        <div class="panel-body mt-5">
            @if ($message = Session::get('success'))
                <div class="alert alert-success alert-dismissible fade show mb-2" role="alert">
                    {{ $message }}
                    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                </div>
                <img src="images/{{ Session::get('image') }}" class="mb-2" style="width:400px;height:200px;">
            @endif
      
            <form action="{{ route('image.store') }}" method="POST" enctype="multipart/form-data">
                @csrf
      
                <div class="mb-3">
                    <label class="form-label" for="inputImage">Select Image:</label>
                    <input 
                        type="file" 
                        name="image" 
                        id="inputImage"
                        class="form-control @error('image') is-invalid @enderror">
      
                    @error('image')
                        <span class="text-danger">{{ $message }}</span>
                    @enderror
                </div>
       
                <div class="mb-3">
                    <button type="submit" class="btn btn-success">Upload</button>
                </div>
       
            </form>
        </div>
    </div>
</div>
</body>
</html>


php artisan serve

http://127.0.0.1:8000/upload-image

