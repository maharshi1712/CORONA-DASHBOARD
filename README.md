<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <script data-ad-client="ca-pub-1321222953625459" async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">
    <link rel="icon" href="logo.png" type="image/icon type">
    <title>CORONA DASHBOARD</title>
    <link rel="stylesheet" href="assets/bootstrap/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Nunito:200,200i,300,300i,400,400i,600,600i,700,700i,800,800i,900,900i">
    <link rel="stylesheet" href="assets/fonts/fontawesome-all.min.css">
    <link rel="stylesheet" href="assets/fonts/font-awesome.min.css">
    <link rel="stylesheet" href="assets/fonts/ionicons.min.css">
    <link rel="stylesheet" href="assets/fonts/simple-line-icons.min.css">
    <link rel="stylesheet" href="assets/fonts/fontawesome5-overrides.min.css">
    <link rel="stylesheet" href="assets/css/dropdown-search-bs4.css">
    <link rel="stylesheet" href="assets/css/Footer-with-social-media-icons.css">
</head>

<body id="page-top" onload="getapi()">
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script>
        
        async function getapi() {
            const response = await fetch("https://api.covid19india.org/state_district_wise.json");
            var data = await response.json();
            var city=document.getElementById('statename').selectedOptions[0].value;
            document.getElementById('statename1').innerText=city;
            console.log(city)
            // console.log(data)
            var data1=data[city].districtData;
            var ActiveCase=[];
            var ConformCase=[];
            var deathCase=[];
            var recoverCase=[];
            var dname=[];
            
            for(i in data1 ){
                dname.push(i);
                ActiveCase.push(data[city].districtData[i].active);
                ConformCase.push(data[city].districtData[i].confirmed);
                deathCase.push(data[city].districtData[i].deceased);
                recoverCase.push(data[city].districtData[i].recovered);
            }
            var activesum=0;
            var recoversum=0;
            var deathsum=0;
            var confirmsum=0;
            for(var i=0;i<ActiveCase.length;i++){
                activesum=activesum+ActiveCase[i]
                recoversum=recoversum+recoverCase[i]
                deathsum=deathsum+deathCase[i]
                confirmsum=confirmsum+ConformCase[i]
            }
            l3=[['District','Total Case']]
            l4=[['District','Total Recover',{role:'style'}]]

            for(var i=0;i<dname.length;i++){
                l3.push([dname[i],ActiveCase[i]]);
                l4.push([dname[i],recoverCase[i],'color:#b8b8b8']);
            }
            console.log(l3)
            document.getElementById('activesum').innerText=activesum;
            document.getElementById('recoversum').innerText=recoversum;
            document.getElementById('deathsum').innerText=deathsum;
            document.getElementById('confirmsum').innerText=confirmsum;
            console.log(ActiveCase);
            console.log(ConformCase);
            console.log(deathCase);
            console.log(dname);
            console.log(recoverCase);

            google.charts.load('current', {'packages':['bar']});
            google.charts.setOnLoadCallback(drawChart);
            google.charts.setOnLoadCallback(drawChart1);

      function drawChart() {
        var data = google.visualization.arrayToDataTable(l3);

        var options = {
          chart: {
            title: 'Total Active Case',
          },
          bars: 'horizontal' // Required for Material Bar Charts.
        };

        var chart = new google.charts.Bar(document.getElementById('barchart_material'));

        chart.draw(data, google.charts.Bar.convertOptions(options));
      }
      function drawChart1() {
        var data = google.visualization.arrayToDataTable(l4);

        var options = {
          chart: {
            title: 'Total Recover Case',
          },
          bars: 'horizontal' // Required for Material Bar Charts.
        };

        var chart = new google.charts.Bar(document.getElementById('barchart_material_1'));

        chart.draw(data, google.charts.Bar.convertOptions(options));
      }
        }
    </script>
    <div id="wrapper">
        <div class="d-flex flex-column" id="content-wrapper">
            <div id="content">
                <nav class="navbar navbar-light navbar-expand bg-white shadow mb-4 topbar static-top">
                    <div class="container-fluid">
                        <select id="statename" style="color: var(--light);background: var(--blue);border: 10px solid var(--blue);border-radius: 5.6px;height: 42.2px;width: 344.6px;" onchange="getapi()">
                            <option value="Andhra Pradesh">Andhra Pradesh</option>
                            <option value="Andaman and Nicobar Islands">Andaman and Nicobar Islands</option>
                            <option value="Arunachal Pradesh">Arunachal Pradesh</option>
                            <option value="Assam">Assam</option>
                            <option value="Bihar">Bihar</option>
                            <option value="Chandigarh">Chandigarh</option>
                            <option value="Chhattisgarh">Chhattisgarh</option>
                            <option value="Dadar and Nagar Haveli">Dadar and Nagar Haveli</option>
                            <option value="Daman and Diu">Daman and Diu</option>
                            <option value="Delhi">Delhi</option>
                            <option value="Lakshadweep">Lakshadweep</option>
                            <option value="Puducherry">Puducherry</option>
                            <option value="Goa">Goa</option>
                            <option value="Gujarat" selected>Gujarat</option>
                            <option value="Haryana">Haryana</option>
                            <option value="Himachal Pradesh">Himachal Pradesh</option>
                            <option value="Jammu and Kashmir">Jammu and Kashmir</option>
                            <option value="Jharkhand">Jharkhand</option>
                            <option value="Karnataka">Karnataka</option>
                            <option value="Kerala">Kerala</option>
                            <option value="Madhya Pradesh">Madhya Pradesh</option>
                            <option value="Maharashtra">Maharashtra</option>
                            <option value="Manipur">Manipur</option>
                            <option value="Meghalaya">Meghalaya</option>
                            <option value="Mizoram">Mizoram</option>
                            <option value="Nagaland">Nagaland</option>
                            <option value="Odisha">Odisha</option>
                            <option value="Punjab">Punjab</option>
                            <option value="Rajasthan">Rajasthan</option>
                            <option value="Sikkim">Sikkim</option>
                            <option value="Tamil Nadu">Tamil Nadu</option>
                            <option value="Telangana">Telangana</option>
                            <option value="Tripura">Tripura</option>
                            <option value="Uttar Pradesh">Uttar Pradesh</option>
                            <option value="Uttarakhand">Uttarakhand</option>
                            <option value="West Bengal">West Bengal</option>
                    </select>
                    
                        <form class="form-inline d-none d-sm-inline-block mr-auto ml-md-3 my-2 my-md-0 mw-100 navbar-search">
                            <div class="input-group">
                                <div class="input-group-append"></div>
                            </div>
                        </form>
                        <ul class="navbar-nav flex-nowrap ml-auto">
                            <li class="nav-item dropdown d-sm-none no-arrow"><a class="dropdown-toggle nav-link" aria-expanded="false" data-toggle="dropdown" href="#"></a>
                                <div class="dropdown-menu dropdown-menu-right p-3 animated--grow-in" aria-labelledby="searchDropdown">
                                    <form class="form-inline mr-auto navbar-search w-100">
                                        <div class="input-group"><input class="bg-light form-control border-0 small" type="text" placeholder="Search for ...">
                                            <div class="input-group-append"><button class="btn btn-primary py-0" type="button"><i class="fas fa-search"></i></button></div>
                                        </div>
                                    </form>
                                </div>
                            </li>
                            <div class="d-none d-sm-block topbar-divider"></div>
                            <li class="nav-item dropdown no-arrow">
                                <div class="nav-item dropdown no-arrow"><a class="dropdown-toggle nav-link" aria-expanded="false" data-toggle="dropdown" href="#"><span class="d-none d-lg-inline mr-2 text-gray-600 small">JAY RATHOD</span><img class="border rounded-circle img-profile" src="logo.png"></a>
                                    <div class="dropdown-menu shadow dropdown-menu-right animated--grow-in"><a class="dropdown-item" href="https://github.com/jkrathod2601/CORONA-DASHBOARD"><i class="fas fa-cogs fa-sm fa-fw mr-2 text-gray-400"></i>&nbsp;CODE</a>
                                        
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </nav>
                <div class="container-fluid">
                    <div class="d-sm-flex justify-content-between align-items-center mb-4">
                        <h3 class="text-dark mb-0" id="statename1">Dashboard</h3>
                    </div>
                    <div class="row">
                        <div class="col-md-12 col-xl-12 mb-4">
                            <div class="card shadow border-left-primary py-2">
                                <div class="card-body">
                                    <div class="row align-items-center no-gutters">
                                        <div class="col mr-2">
                                            <div class="text-uppercase text-primary font-weight-bold text-xs mb-1"><span>TOTAL&nbsp;ACTIVE CASE</span></div>
                                            <div class="text-dark font-weight-bold h5 mb-0"><span id="activesum">WAITING FOR DATA...</span></div>
                                        </div>
                                        <div class="col-auto"><i class="icon ion-ios-contact-outline fa-2x text-gray-300"></i></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-12 col-xl-12 mb-4">
                            <div class="card shadow border-left-success py-2">
                                <div class="card-body">
                                    <div class="row align-items-center no-gutters">
                                        <div class="col mr-2">
                                            <div class="text-uppercase text-success font-weight-bold text-xs mb-1"><span>TOTAL RECOVER</span></div>
                                            <div class="text-dark font-weight-bold h5 mb-0"><span id="recoversum">WAITING FOR DATA...</span></div>
                                        </div>
                                        <div class="col-auto"><i class="icon-user-follow fa-2x text-gray-300"></i></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-12 col-xl-12 mb-4">
                            <div class="card shadow border-left-info py-2">
                                <div class="card-body">
                                    <div class="row align-items-center no-gutters">
                                        <div class="col mr-2">
                                            <div class="text-uppercase text-info font-weight-bold text-xs mb-1"><span>TOTAL&nbsp; DEATH</span></div>
                                            <div class="row no-gutters align-items-center">
                                                <div class="col-auto">
                                                    <div class="text-dark font-weight-bold h5 mb-0 mr-3"><span id="deathsum">WAITING FOR DATA...</span></div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-auto"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" class="fa-2x text-gray-300">
                                                <path d="M12 6C12.5523 6 13 6.44772 13 7V13C13 13.5523 12.5523 14 12 14C11.4477 14 11 13.5523 11 13V7C11 6.44772 11.4477 6 12 6Z" fill="currentColor"></path>
                                                <path d="M12 16C11.4477 16 11 16.4477 11 17C11 17.5523 11.4477 18 12 18C12.5523 18 13 17.5523 13 17C13 16.4477 12.5523 16 12 16Z" fill="currentColor"></path>
                                                <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C6.47715 2 2 6.47715 2 12C2 17.5228 6.47715 22 12 22C17.5228 22 22 17.5228 22 12C22 6.47715 17.5228 2 12 2ZM4 12C4 16.4183 7.58172 20 12 20C16.4183 20 20 16.4183 20 12C20 7.58172 16.4183 4 12 4C7.58172 4 4 7.58172 4 12Z" fill="currentColor"></path>
                                            </svg></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-12 col-xl-12 mb-4">
                            <div class="card shadow border-left-warning py-2">
                                <div class="card-body">
                                    <div class="row align-items-center no-gutters">
                                        <div class="col mr-2">
                                            <div class="text-uppercase text-warning font-weight-bold text-xs mb-1"><span>TOTAL CONFIRM</span></div>
                                            <div class="text-dark font-weight-bold h5 mb-0"><span id="confirmsum">WAITING FOR DATA...</span></div>
                                        </div>
                                        <div class="col-auto"><i class="fas fa-comments fa-2x text-gray-300"></i></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-12 col-xl-12 mb-4">
                <div class="card shadow border-left-primary py-2">
                    <div class="card-body">
                        <div class="row align-items-center no-gutters">
                            <div id="barchart_material" style="width: 900px; height: 500px;"></div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-12 col-xl-12 mb-4">
                <div class="card shadow border-left-primary py-2">
                    <div class="card-body">
                        <div class="row align-items-center no-gutters">
                            <div id="barchart_material_1" style="width: 900px; height: 500px;"></div>
                        </div>
                    </div>
                </div>
            </div>
           
            <footer class="bg-white sticky-footer">
                <div class="container my-auto">
                    <div class="text-center my-auto copyright">
                        <footer class="bg-light shadow-sm" id="footerpad" style="background: var(--light);height: 149.725px;padding: 26px 0px 20px;margin: -29px;">
                            <div class="container">
                                <div class="row">
                                    <div class="col-md-6 col-lg-8 mx-auto">
                                        <ul class="list-inline text-center">
                                            <li class="list-inline-item"><a href="https://github.com/jkrathod2601"><span class="fa-stack fa-lg"><i class="fa fa-circle fa-stack-2x"></i><i class="fa fa-github fa-stack-1x fa-inverse"></i></span></a></li>
                                            <li class="list-inline-item"><a href="https://twitter.com/JayRath88875779"><span class="fa-stack fa-lg"><i class="fa fa-circle fa-stack-2x"></i><i class="fa fa-twitter fa-stack-1x fa-inverse"></i></span></a></li>
                                            <li class="list-inline-item"><a href="https://www.instagram.com/_jay_26_01/"><span class="fa-stack fa-lg"><i class="fa fa-circle fa-stack-2x"></i><i class="fa fa-instagram fa-stack-1x fa-inverse"></i></span></a></li>
                                            <li class="list-inline-item"><a href="https://api.whatsapp.com/send?phone=+917201064761&amp;text=Hey Chintan,I am "><span class="fa-stack fa-lg"><i class="fa fa-circle fa-stack-2x"></i><i class="fa fa-whatsapp fa-stack-1x fa-inverse"></i></span></a></li>
                                        </ul><p class="copyright text-muted text-center">THANK YOU FOR VISITING </p>
                                    </div>
                                </div>
                            </div>
                        </footer><span></span>
                    </div>
                </div>
            </footer>
        </div><a class="border rounded d-inline scroll-to-top" href="#page-top"><i class="fas fa-angle-up"></i></a>
    </div>
    <script src="assets/js/jquery.min.js"></script>
    <script src="assets/bootstrap/js/bootstrap.min.js"></script>
    <script src="assets/js/dropdown-search-bs4.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.4.1/jquery.easing.js"></script>
    <script src="assets/js/theme.js"></script>
</body>

</html>
