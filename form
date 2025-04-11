<?php
$showAlert = false;
$showError = false;

include '_dbconnect.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
   
    if (isset($_POST['delete_id'])) {
        $delete_id = $_POST['delete_id'];

        $delete_sql = "DELETE FROM `form` WHERE id = ?";
        $stmt = mysqli_prepare($conn, $delete_sql);
        mysqli_stmt_bind_param($stmt, "i", $delete_id);
        
        if (mysqli_stmt_execute($stmt)) {
            echo "<p style='color:green;'> $delete_id deleted successfully.</p>";
        } else {
            echo "<p style='color:red;'> Error deleting task: " . mysqli_error($conn) . "</p>";
        }

        mysqli_stmt_close($stmt);
    }
    
    else if (isset($_POST['title'])) {
        $title = $_POST["title"];
        $description = $_POST["description"];
        $priority = $_POST["priority"];
        $status = $_POST["status"];
        $duedate = $_POST["duedate"];
        $tag = $_POST["tag"];

        $sql = "INSERT INTO `form` (`title`, `description`, `priority`, `status`, `duedate`, `tag`) 
                VALUES ('$title', '$description', '$priority', '$status', '$duedate', '$tag')";
        $result = mysqli_query($conn, $sql);

        if ($result) {
            $showAlert = true;
        } else {
            $showError = "Error inserting data.";
        }
    }
}
?>


<!doctype html>
<html lang="en">
  <head>
  
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

   
     <title>TODO LIST</title>
     <style>
    body {
        font-family: sans-serif;
        padding: 20px;
    }

    form {
        max-width: 400px;
        margin: 0 auto;
    }

    label {
        display: block;
        margin-top: 10px;
        margin-bottom: 5px;
    }

    input[type="text"],
    input[type="date"],
    textarea {
        width: 100%;
        padding: 6px;
        margin-bottom: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
    }

    input[type="submit"] {
        padding: 8px 16px;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    input[type="submit"]:hover {
        background-color: #0056b3;
    }
</style>

  </head>
  <body>
   
    <?php
    if($showAlert){
    echo ' <div class="alert alert-success alert-dismissible fade show" role="alert">
        <strong>Success!</strong>
        <button type="button" class="close" data-dismiss="alert" aria-label="Close">
            <span aria-hidden="true">×</span>
        </button>
    </div> ';
    }
    if($showError){
    echo ' <div class="alert alert-danger alert-dismissible fade show" role="alert">
        <strong>Error!</strong> '. $showError.'
        <button type="button" class="close" data-dismiss="alert" aria-label="Close">
            <span aria-hidden="true">×</span>
        </button>
    </div> ';
    }
    ?>
      <div class="container">
        <h1>form</h1>
        <form action="/DSA/srmu/form.php" method="POST">
            <label for="title">title:</label>
            <input type="text" id="title" name="title" required><br>
            
            <label for="description">description:</label>
            <textarea id="description" name="description" required></textarea><br>

            <label for="priority">priority:</label>
            <textarea id="priority" name="priority" required></textarea><br>

            <label for="status">status:</label>
            <textarea id="status" name="status" required></textarea><br>

            <label for="duedate">duedate:</label>
            <textarea id="duedate" name="duedate"></textarea><br>

            <label for="tag">tag:</label>
            <textarea id="tag" name="tag"></textarea><br>

            <input type="submit" value="submit">
        </form>
</div>
<hr>
<h2>Delete a Task</h2>
<form action="/DSA/srmu/form.php" method="POST">
    <label for="delete_id">Enter Task ID to Delete:</label>
    <input type="number" id="delete_id" name="delete_id" required>
    <input type="submit" value="Delete Task">
</form>
<hr>
<h2>show</h2>

<table >
    <tr style="background-color: #f2f2f2;">
        <th>ID</th>
        <th>Title</th>
        <th>Description</th>
        <th>Priority</th>
        <th>Status</th>
        <th>Due Date</th>
        <th>Tag</th>
    </tr>

<?php
include '_dbconnect.php';

$sql = "SELECT * FROM `form` ORDER BY id DESC";
$result = mysqli_query($conn, $sql);

if (mysqli_num_rows($result) > 0) {
    while($row = mysqli_fetch_assoc($result)) {
        echo "<tr>";
        echo "<td>" . $row['id'] . "</td>";
        echo "<td>" . htmlspecialchars($row['title']) . "</td>";
        echo "<td>" . htmlspecialchars($row['description']) . "</td>";
        echo "<td>" . htmlspecialchars($row['priority']) . "</td>";
        echo "<td>" . htmlspecialchars($row['status']) . "</td>";
        echo "<td>" . htmlspecialchars($row['duedate']) . "</td>";
        echo "<td>" . htmlspecialchars($row['tag']) . "</td>";
        echo "</tr>";
    }
} else {
    echo "<tr><td colspan='7' style='text-align:center;'>No tasks found.</td></tr>";
}
?>
</table>

   </body>
</html>






