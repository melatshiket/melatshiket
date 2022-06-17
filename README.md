- 👋 Hi, I’m @melatshiket
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
melatshiket/melatshiket is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

<?php require_once "controllerUserData.php"; ?>
<?php 
$email = $_SESSION['email'];
$password = $_SESSION['password'];
if($email != false && $password != false){
    $sql = "SELECT * FROM usertable WHERE email = '$email'";
    $run_Sql = mysqli_query($con, $sql);
    if($run_Sql){
        $fetch_info = mysqli_fetch_assoc($run_Sql);
        $status = $fetch_info['status'];
        $code = $fetch_info['code'];
        $role=$fetch_info['role'];

        if($status == "verified"){
            if($code != 0){
                header('Location: reset-code.php');
            }
        }else{
  header('Location: user-otp.php');
        }
    }
}else{
    header('Location: login-user.php');
    // header('Location: signup-user.php');

}
?> 
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
        <meta name="description" content="" />
        <meta name="author" content="" />
        <title>Coordinator Dashboard</title>
        <link href="style.css" rel="stylesheet" />
        <link href="css/styles.css" rel="stylesheet" />
        <script src="js/all.min.js" crossorigin="anonymous"></script>
        <style>
            #count{
                border-radius: 50%;
                position: relative;
                top: -10px;
                left: -10px;
            }
        </style>
    </head>
    <body class="sb-nav-fixed">
        <nav class="sb-topnav navbar navbar-expand navbar-dark bg-primary">
            <!-- Navbar Brand-->
        
            <a class="navbar-brand ps-0" href=""><h4>Coordinator Panel</h4></a>
            
      
            <!-- Sidebar Toggle-->
            <button class="btn btn-link btn-sm order-1 order-lg-0 me-4 me-lg-0" id="sidebarToggle" href="#!"><i class="fas fa-bars"></i></button>
            <!-- Navbar Search-->
            <h2 class="navbar-brand ps-0">Welcome to Training Management system</h2>
         
            <form class="d-none d-md-inline-block form-inline ms-auto me-0 me-md-3 my-2 my-md-0">
                <div class="input-group">
  
                <!-- <input class="form-control" type="text" placeholder=" " aria-label="Search for..." aria-describedby="btnNavbarSearch" /> -->
                <!-- <button class="btn btn-primary" id="btnNavbarSearch" type="hidden"><i class="fas fa-search"></i></button> -->
                <input class="form-control" type="hidden" name="cpassword" placeholder="Confirm password" required>
     </div>
            </form>
          <?php  
                            
                            $name= $fetch_info['name'];
                              $user="root";
  $password="";
  $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
  mysqli_select_db($connection,"tms");
  
  $query="SElect count(ID) as total from feedback where recieverName='$name' and status='0'";
  $query_run=mysqli_query($connection,$query);
  $values=mysqli_fetch_assoc($query_run);
  $num=$values['total'];
  ?>
            <!-- notify -->
            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                <li class="nav-item dropdown">
                    <?php
                      $query="SElect *from feedback where recieverName='$name' and status='0'";
                      $query_run=mysqli_query($connection,$query);
                    ?>
                <a class="nav-link dropdown-toggle" id="feedback" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false"><i class="fas fa-envelope fa-fw"></i><span style="color: rgb(233, 34, 34);" id="count"><?php echo $num?></span></a>
                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                    <?php  
                            
                            $name= $fetch_info['name'];
                              $user="root";
  $password="";
  $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
  mysqli_select_db($connection,"tms");
  

  if(mysqli_num_rows($query_run) > 0){
      foreach($query_run as $item){
          ?>
         <li><?php echo $item["comment"]?></li>

          <?php

      }
  }
  
  ?> 
                   
                    </ul>
                </li>
            </ul>
            <!-- notify end -->
            <!-- Navbar-->
           
                
                    
                
            </ul>
            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false"><i class=""></i><h5 style="color: aliceblue;"><?php echo $fetch_info['name'] ?></h5> </a>                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                        <li><a class="dropdown-item" href="#!">
        </a></li>
                        <li><hr class="dropdown-divider" /></li>
                        <li><a class="dropdown-item" href="logout-user.php">Logout</a></li>
                    </ul>
                    
                </li>
            </ul>
        </nav>
        
        <div id="layoutSidenav">
            <div id="layoutSidenav_nav">
                <nav class="sb-sidenav accordion sb-sidenav-dark" id="sidenavAccordion">
                    <div class="sb-sidenav-menu">
                        <div class="nav">
                            <!-- <a class="nav-link" href="">
                                <div class="sb-nav-link-icon"><i class="fas fa-tachometer-alt"></i></div>
                                Coordinator 
     
                            </a> -->
</br>
                          
                        <!-- start new sidebar -->
<a class="nav-link" href="dashboard.php">
                                <div class="sb-nav-link-icon"><i class="fas fa-tachometer-alt"></i></div>
                                
                                <?php
                                    $date=date('y-m-d h:i:s');
                               echo $date;
                                ?>
                            </a>
                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false"> &nbsp;&nbsp;<i class="fas fa-user fa-fw"></i>&nbsp;Manage User</a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="signup-user.php">Add User</a></li>
                                        <!-- <li><a class="dropdown-item" href="Allusers.php">Add all  Users</a></li> -->
                                        <li><a class="dropdown-item" href="usersview.php">View all  Users</a></li>

                                        <li><a class="dropdown-item" href="profile.php">View all  Users profile</a></li>

                                    </ul>
                                </li>
                            </ul>
                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">   &nbsp;&nbsp;<i class="fas fa-table fa-fw"></i>&nbsp;Manage Schedule </a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="schedule.php">Add Schedule</a></li>
                                        <li><a class="dropdown-item" href="scheduleview.php">View Schedule</a></li>
                                     
                                    </ul>
                                </li>
                            </ul>
                           
                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">   &nbsp;&nbsp;<i class="fas fa-columns fa-fw"></i>&nbsp;Manage Plan </a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="plan.php">Add Plan</a></li>
                                        <li><a class="dropdown-item" href="planview.php">View plan</a></li>
                                     
                                    </ul>
                                </li>
                            </ul>
                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">  &nbsp; &nbsp;<i class="fas fa-chart-bar fa-fw"></i> &nbsp; Manage Report </a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="report2.php">Generate Report</a></li>
                                        <li><a class="dropdown-item" href="reportTable.php">Generate  Report in table</a></li>
                                        <li><a class="dropdown-item" href="report3.php">Report all users in percent</a></li>

                                        <li><a class="dropdown-item" href="#!"></a></li>
                                     
                                    </ul>
                                </li>
                            </ul>
                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">

<a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false"> &nbsp;&nbsp; <i class="fas fa-envelope fa-fw"></i>&nbsp;Manage Feedback</a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="Feedback.php">Send Feedback</a></li>
                                        <li><a class="dropdown-item" href="feedbackview.php">View Feedback</a></li>
                                     
                                    </ul>
                                </li>
                            </ul>
                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false"> &nbsp;&nbsp; <i class="fas fa-chart-area fa-fw"></i>&nbsp;Manage Topic</a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="Topic.php">Add Topic</a></li>
                                        <li><a class="dropdown-item" href="Topicview.php">View Topic</a></li>
                                     
                                    </ul>
                                </li>
                            </ul>

                            <ul class="navbar-nav ms-auto ms-md-0 me-3 me-lg-4">
                               
                                <li class="nav-item dropdown">
                                    <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false"> &nbsp;&nbsp; <i class="fas fa-chart-area fa-fw"></i>&nbsp;Topic Selection</a>
                                    <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                        <li><a class="dropdown-item" href="selectionview.php">view selection</a></li>
                                        <li><a class="dropdown-item" href="ranking.php">view ranking</a></li>

                                        <!-- <li><a class="dropdown-item" href="Topicview.php">View Topic</a></li> -->
                                     
                                    </ul>
                                </li>
                            </ul>
                        <!-- end new side bar -->
                            
                                        <!-- Trainer manage-->
                                        <!-- <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#collapsePages" aria-expanded="false" aria-controls="collapsePages">
                                            <div class="sb-nav-link-icon"><i class="fas fa-book-open"></i></div>
                                       Manage
                                            <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
                                        </a> -->
                                                                                <!-- account manage starts-->
                                        <div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
                                            <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
                                                <a class="nav-link collapsed" href="user2.php" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
                                                Manage Account
                                                    <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
                                                </a>
                                                <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
                                                    <nav class="sb-sidenav-menu-nested nav">
                        
                                                        <!-- <a class="nav-link" href="user.html">Add User</a> -->
                                                        <a class="nav-link" href="user2.php">Add User</a>
                                                        <a class="nav-link" href="user.html">Add User</a>
                                                        <a class="nav-link" href="indextext.php">textindex</a>





                                                        <a class="nav-link" href="viewusers.php">view users</a>
                                                    </nav>
                                                </div>
                                                
                                            </nav>
                                        </div>
                                                                                 <!-- account  manage ends -->


                                        <div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
                                            <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
                                                <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
                                                Manage Trainer
                                                    <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
                                                </a>
                                                <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
                                                    <nav class="sb-sidenav-menu-nested nav">
                        
                                                        <a class="nav-link" href="trainerreg.php">Add Trainer</a>
                                                        <a class="nav-link" href="viewtrainer.php">view Trainer</a>
                                                    </nav>
                                                </div>
                                                
                                            </nav>
                                        </div>
                  <!-- Trainer manage ends--
                     <!.... Trainee manage start-->
                 
                    <div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
                        <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
                            <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
                            Manage Trainee
                                <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
                            </a>
                            <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
                                <nav class="sb-sidenav-menu-nested nav">
    
                                    <a class="nav-link" href="traineereg.php">Add Trainee</a>
                                    <a class="nav-link" href="viewtrainee.php">view Trainee</a>
                                </nav>
                            </div>
                            
                        </nav>
                    </div>
                     <!-- Trainee manage ends-->

 <!-- schedule manage starts-->
 <div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
    <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
        <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
        Manage schedule
            <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
        </a>
        <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
            <nav class="sb-sidenav-menu-nested nav">

                <a class="nav-link" href="schedulereg.html">Add schedule</a>
                <a class="nav-link" href="">view schedule</a>
            </nav>
        </div>
        
    </nav>
</div>
 <!-- schedule manage ends-->

<!-- plan manage starts-->
<div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
    <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
        <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
        Manage plan
            <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
        </a>
        <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
            <nav class="sb-sidenav-menu-nested nav">

                <a class="nav-link" href="planreg.html">set plan</a>
                <a class="nav-link" href="">view plan</a>
            </nav>
        </div>
        
    </nav>
</div>
 <!-- plan manage ends-->
<!-- Report manage starts-->
<div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
    <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
        <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
        Manage Report
            <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
        </a>
        <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
            <nav class="sb-sidenav-menu-nested nav">

                <a class="nav-link" href="">Generate Report</a>
                <a class="nav-link" href="">view Report</a>
            </nav>
        </div>
        
    </nav>
</div>
 <!-- report manage ends-->
<!-- topic manage starts-->
<div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
    <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
        <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
        Manage topic
    
            <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
        </a>
        <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
            <nav class="sb-sidenav-menu-nested nav">

                <a class="nav-link" href="addTopic.php">Add Topic</a>
                <a class="nav-link" href="viewtopic.php">view Topic</a>
            </nav>
        </div>
        
    </nav>
</div>
 <!-- topic manage ends-->
 <!-- feedback manage starts-->
 <div class="collapse" id="collapsePages" aria-labelledby="headingTwo" data-bs-parent="#sidenavAccordion">
    <nav class="sb-sidenav-menu-nested nav accordion" id="sidenavAccordionPages">
        <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#pagesCollapseAuth" aria-expanded="false" aria-controls="pagesCollapseAuth">
     Manage Feedback
    
            <div class="sb-sidenav-collapse-arrow"><i class="fas fa-angle-down"></i></div>
        </a>
        <div class="collapse" id="pagesCollapseAuth" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordionPages">
            <nav class="sb-sidenav-menu-nested nav">

                <a class="nav-link" href="feedbackreg.html">send Feedback</a>
                <a class="nav-link" href="">view Feedback</a>
            </nav>
        </div>
        
    </nav>
</div>
 <!-- feedback manage ends-->
                        </div>
                    </div>
                    <div class="sb-sidenav-footer">
                        <div class="small">Logged in as Coordinator:</div>
                        
                    </div>
                </nav>
            </div>
            <div id="layoutSidenav_content">
                <main>
                    <div class="container-fluid  px-8">
                       
                        <ol class="breadcrumb mb-4">
                            <li class="breadcrumb-item active"></li>
                        </ol>
                        <div class="row">
                            <div class="col-xl-3 col-md-6">
                                <div class="card bg-primary text-white mb-4">
                                    <div class="card-body">Users Information</div>
                                    <div class="card-footer d-flex align-items-center justify-content-between">
                                        <?php
                                    $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");



$all="select count(ID) as total from usertable";
$result=mysqli_query($connection,$all);
$values=mysqli_fetch_assoc($result);
$num_rows1=$values['total'];
echo "Total there is &nbsp;".$num_rows1."&nbsp;Users";
?></br>
                                        <!-- <a class="small text-white stretched-link" href="#">View Details</a> -->
                                        <!-- <div class="small text-white"><i class="fas fa-angle-right"></i></div> -->
                                    </div>
                                </div>
                            </div>
                            <div class="col-xl-3 col-md-6">
                                <div class="card bg-warning text-white mb-4">
                                    <div class="card-body">Training Schedule Information</div>

                                    <div class="card-footer d-flex align-items-center justify-content-between">
                                    <?php
                                    $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");



$all="select count(ID) as total from schedule";
$result=mysqli_query($connection,$all);
$values=mysqli_fetch_assoc($result);
$num_rows1=$values['total'];
echo "Total there is &nbsp;".$num_rows1."&nbsp;Schedule";
?></br>
</br>
                                        <!-- <a class="small text-white stretched-link" href="#">View Details</a> -->
                                        <div class="small text-white"><i class="fas fa-angle-right"></i></div>
                                    </div>
                                </div>
                            </div>
                            <div class="col-xl-3 col-md-6">
                                <div class="card bg-success text-white mb-4">
                                    <div class="card-body">Topic Information</div>
                                    <div class="card-footer d-flex align-items-center justify-content-between">
                                    <?php
                                    $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");



$all="select count(ID) as total from topic";
$result=mysqli_query($connection,$all);
$values=mysqli_fetch_assoc($result);
$num_rows1=$values['total'];
echo "Total there is &nbsp;".$num_rows1."&nbsp;Topic";
?></br>
                                        <!-- <a class="small text-white stretched-link" href="#">View Details</a> -->
                                        <!-- <div class="small text-white"><i class="fas fa-angle-right"></i></div> -->
                                    </div>
                                </div>
                            </div>
                            <!-- users varified -->
                            <div class="col-xl-3 col-md-6">
                                <div class="card bg-success text-white mb-4">
                                    <div class="card-body">Users verified</div>
                                    <div class="card-footer d-flex align-items-center justify-content-between">
                                    <?php
                                    $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");



$all="select count(ID) as total from usertable where status='verified'";
$result=mysqli_query($connection,$all);
$values=mysqli_fetch_assoc($result);
$num_rows1=$values['total'];
echo "Total there is &nbsp;".$num_rows1."&nbsp;Users Verified";
?></br>
                                        <!-- <a class="small text-white stretched-link" href="#">View Details</a> -->
                                        <!-- <div class="small text-white"><i class="fas fa-angle-right"></i></div> -->
                                    </div>
                                </div>
                            </div>
                            <!-- plan dashbord -->

                            <div class="col-xl-3 col-md-6">
                                <div class="card bg-success text-white mb-4">
                                    <div class="card-body">Plan Information</div>
                                    <div class="card-footer d-flex align-items-center justify-content-between">
                                    <?php
                                    $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");



$all="select count(ID) as total from plan";
$result=mysqli_query($connection,$all);
$values=mysqli_fetch_assoc($result);
$num_rows1=$values['total'];
echo "Total there is &nbsp;".$num_rows1."&nbsp;Plan";
?></br>
                                        <!-- <a class="small text-white stretched-link" href="#">View Details</a> -->
                                        <!-- <div class="small text-white"><i class="fas fa-angle-right"></i></div> -->
                                    </div>
                                </div>
                            </div>
                            <div class="col-xl-3 col-md-6">
                                <div class="card bg-danger text-white mb-4">
                                    <div class="card-body">Users Not verified</div>
                                    <div class="card-footer d-flex align-items-center justify-content-between">
                                    <?php
                                    $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");



$all="select count(ID) as total from usertable where status='notverified'";
$result=mysqli_query($connection,$all);
$values=mysqli_fetch_assoc($result);
$num_rows1=$values['total'];
echo "Total  &nbsp;".$num_rows1."&nbsp;users not verified";
?></br>
                                        <!-- <a class="small text-white stretched-link" href="#">View Details</a> -->
                                        <!-- <div class="small text-white"><i class="fas fa-angle-right"></i></div> -->
                                    </div>
                                </div>
                            </div>
                        </div>
                        <?php
                        $user="root";
 $password="";
 $connection=mysqli_connect("localhost",$user,$password) or die("couldn't connect,".mysqli_error());
 mysqli_select_db($connection,"tms");
 $date=date('y-m-d');

 $sql = "SELECT * from schedule where ID=10";
 $run_Sql = mysqli_query($con, $sql);
 if($run_Sql){
     $fetch_info = mysqli_fetch_assoc($run_Sql);
     $status = $fetch_info['Trainingstartdate'];
     $enddate = $fetch_info['Trainingenddate'];
     $topic=$fetch_info['TopicName'];

    
 
 }
 echo $date;
 echo $status;
 echo $enddate;
 echo"<br>";
 echo $name;
 $dateee=$status;
 $ends=$enddate;
 echo $role;
 $_SESSION['$status status']="schedule is in progress   ";
 $_SESSION['status_code']="success";
 
 echo"<br>";
 if($dateee == '2022-06-11')
 {
    // $_SESSION['status']="Training is progress";
    $_SESSION['status_code']="success";

 }
 else{
    $_SESSION['status']="There is no Training which is in progress";
 $_SESSION['status_code']="error";


 }
//  echo $ends;
//  if($status < $date)
//  {
//      $_SESSION['$status status']="schedule is in progress   ";
//      $_SESSION['status_code']="success";
//  }
//  else
//  {
//      $_SESSION['status']="schedule is passed   ";
//      $_SESSION['status_code']="error";
 
//  }
 ?>
                        <!-- <div class="row">
                            <div class="col-xl-6">
                                <div class="card mb-4">
                                    <div class="card-header">
                                        <i class="fas fa-chart-area me-1"></i>
                                        Area Chart Example
                                    </div>
                                    <div class="card-body"><canvas id="myAreaChart" width="100%" height="40"></canvas></div>
                                </div>
                            </div>
                            <div class="col-xl-6">
                                <div class="card mb-4">
                                    <div class="card-header">
                                        <i class="fas fa-chart-bar me-1"></i>
                                        Bar Chart Example
                                    </div>
                                    <div class="card-body"><canvas id="myBarChart" width="100%" height="40"></canvas></div>
                                </div>
                            </div>
                        </div> -->



                      
                       
                        <div class="card mb-4">
                            <div class="card-header">
                                <!-- <i class="fas fa-table me-1"></i> -->
</br></br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>




                               Coordinator List Example
                             <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
  Add Trainer
</button>  

 Modal
<?php
echo $role;
?>
<input type="text" value="<?php echo $name;?>">
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <?php
        $name=$fetch_info['name'];
        echo $name
        ?>
        <h5 class="modal-title" id="exampleModalLabel">Profile Form</h5>
        <?php
        $name=$fetch_info['name'];
        echo $name
        ?>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
         <form method="POST" enctype="multipart/form-data">
            <?php
            echo $name;
            ?>
            <div class="mb-3">
                
                  <input type="text" class="form-control" id="" name="name" placeholder="Enter Fname" value="<?php echo $fetch_info['name'];?>">
           </div>
               <div class="mb-3">
                
                  <input type="email" class="form-control" id="exampleFormControlInput1" name="email" value="<?php echo $fetch_info['email'];?>" placeholder="Enter Email addres">
               </div>
            <div class="mb-3">
               
                <input type="number" class="form-control" id="exampleFormControlInput1" name="password" placeholder="Enter phone number">
              </div>
              <div class="mb-3">
             
                 <input type="text" class="form-control" id="exampleFormControlInput1" name="cpassword" placeholder="Enter Address ">
               </div>
               <div class="mb-3">
             <input type="number" class="form-control" id="exampleFormControlInput1" name="cpassword" placeholder="Enter your age ">
           </div>

           <div class="mb-3">
               <select name="gender" id="" class="form-select" aria-label="Default select example">
                           <option selected disabled >--select sex--</option>
                           <option value="Male">Male</option>
                           <option value="Female">Female</option>
                        </select>
                 <!-- <input type="password" class="form-control" id="exampleFormControlInput1" name="cpassword" placeholder="Enter Email addres"> -->
               </div>
               <div class="mb-3">
              
               <div class="mb-3">
             
             <input type="file" class="form-control" id="exampleFormControlInput1" name="faculty_image"  required "">
           </div>
           <div class="mb-3">





                        
                        <!-- <input class="form-control" type="text" name="role" placeholder="enter role" required value""> -->
                  
              
              <!-- <div class="mb-3">
        textarea
                <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
              </div> -->
        </div>
        <div class="modal-footer">
      
            
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="submit" name="signup" class="btn btn-primary">Save </button> 
          <!-- <button type="submit" class="btn btn-primary" name="addtrainee">save</button> -->

          <!-- <input class="form-control button" type="submit" name="signup" value="Signup"> -->

        </div>
  </Form>
      </div>
      
    </div>
  </div>
</div>
                              
                            </div>
                            <div class="card-body">
                                <?php

                                ?>
                                <table id="datatablesSimple">
                                    <thead>
                                        <tr>
                                            
                                            <th>FName</th>
                                            <th>LName</th>
                                            <th>Age</th>
                                            <th>Address</th>
                                            <th>Email</th>
                                            <th>Gender</th>
                                            <th>Edit</th>
                                            <th>Delete</th>


                                        </tr>
                                    </thead>
                                    <tfoot>
                                        <tr>
                                            <th>Name</th>
                                            <th>Position</th>
                                            <th>Office</th>
                                            <th>Age</th>
                                            <th>Start date</th>
                                            <th>Salary</th>
                                        </tr>
                                    </tfoot>
                                    <tbody>
                                        <tr>
                                            <td>Abebe</td>
                                            <td>Tirka</td>
                                            <td>20</td>
                                            <td>Hawassa</td>
                                            <td>abe4@gmail.com</td>
                                            <td>Male</td>
                                            <td>
                                                <button type="submit" class="btn btn-success">Edit</button>

                                            </td>
                                            <td>
                                                <button type="submit" class="btn btn-danger">Delete</button>

                                            </td>

                                            

                                        </tr>
                                       
                                        <tr>
                                            <td>Abebe</td>
                                            <td>Huramo</td>
                                            <td>20</td>
                                            <td>wolkite</td>
                                            <td>abetys4@gmail.com</td>
                                            <td>Male</td>
                                            <td>
                                                <button type="submit" class="btn btn-success">Edit</button>

                                            </td>
                                            <td>
                                                <button type="submit" class="btn btn-danger">Delete</button>

                                            </td>
                                        </tr>
                                        <tr>
                                            <td>meseret</td>
                                            <td>Tirka</td>
                                            <td>20</td>
                                            <td>Addisabeba</td>
                                            <td>abe4@gmail.com</td>
                                            <td>Female</td>
                                            <td>
                                                <button type="submit" class="btn btn-success">Edit</button>

                                            </td>
                                            <td>
                                                <button type="submit" class="btn btn-danger">Delete</button>

                                            </td>
                                        </tr>
                                        <tr>
                                            <td>John</td>
                                            <td>Temesgen</td>
                                            <td>20</td>
                                            <td>Addisabeba</td>
                                            <td>abe4@gmail.com</td>
                                            <td>Male</td>
                                            <td>
                                                <button type="submit" class="btn btn-success">Edit</button>

                                            </td>
                                            <td>
                                                <button type="submit" class="btn btn-danger">Delete</button>

                                            </td>
                                        </tr>
                                        <tr>
                                            <td>Isreal</td>
                                            <td>Daniel</td>
                                            <td>20</td>
                                            <td>Addisabeba</td>
                                            <td>isrobe4@gmail.com</td>
                                            <td>Male</td>
                                            <td>
                                                <button type="submit" class="btn btn-success">Edit</button>

                                            </td>
                                            <td>
                                                <button type="submit" class="btn btn-danger">Delete</button>

                                            </td>
                                        </tr>
                                       
                                       
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </main>
                <footer class="py-4 bg-light mt-auto">
                    <div class="container-fluid px-4">
                        <div class="d-flex align-items-center justify-content-between small">
                            <div class="text-muted">Copyright &copy; Fourth Year Information System</div>
                            <div>
                                <a href="#">Privacy Policy</a>
                                &middot;
                                <a href="#">Terms &amp; Conditions</a>
                            </div>
                        </div>
                    </div>
                </footer>
            </div>
        </div>
        <!-- fro dropdown  -->
        <script src="js/bootstrap.bundle.min.js" crossorigin="anonymous"></script>
        <script src="js/scripts.js"></script>
        <script src="js/Chart.min.js" crossorigin="anonymous"></script>
        <script src="assets/demo/chart-area-demo.js"></script>
        <script src="assets/demo/chart-bar-demo.js"></script>
                <!-- fro table search icons  -->
        <script src="js/simple-datatables@latest.js" crossorigin="anonymous"></script>
        <script src="js/datatables-simple-demo.js"></script>
        <script src="js/sweetalert.min.js"></script>
        <?php
         if(isset($_SESSION['status']) && $_SESSION['status']!='' )
         {
             ?>
             <!-- echo '<h2 class="bg-primary">'.$_SESSION['insert'].'</h2>'; -->
             <script>
            swal({
  title: "<?php echo$_SESSION['status']?>!",
//    text: "You clicked the button!",
  icon: "<?php echo $_SESSION['status_code']?>",
 button: "ok!",
 });
   </script>
             <?php
             unset($_SESSION['status']);
         }
        ?>
        <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
        <script>
            $(document).ready(function(){
          $("#feedback").on("click",function(){
$.ajax({
url: "readfeedback.php",
success: function(res){
    console.log(res);
}
});
          });

            })
        </script>
    </body>
</html>

