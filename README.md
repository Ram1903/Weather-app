# Weather-app
Weather  app using Javascript , HTML and Css
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <link
      href="https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500&display=swap"
      rel="stylesheet"
    />

    <style>
      * {
        padding: 0;
        margin: 0;
        /* font-family: "Jost", sans-serif; */
        font-family: "Quicksand", sans-serif;
      }

      body {
        background: #f3f2ef;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        height: 100vh;
        width: 100vw;
      }

      html,
      body {
        font-size: 62.5%;
        height: 100%;
      }

      html {
        background: #eee;
      }

      .box {
        width: 20vw;
        height: 60vh;
        border-radius: 0.5rem;
        box-shadow: 0 0.2rem 3rem rgba(0, 0, 0, 0.2);
        background: #a5bbdd;
        position: relative;
        overflow: hidden;
        transform: translate3d(0, 0, 0);
        min-width: 20rem;
        min-height: 35rem;
      }

      .wave {
        opacity: 0.3;
        position: absolute;
        top: 120%;
        left: 50%;
        background: white;
        width: 50rem;
        height: 50rem;
        margin-left: -25rem;
        margin-top: -25rem;
        transform-origin: 50% 48%;
        border-radius: 43%;
        animation: drift 3000ms infinite linear;
        z-index: 1;
      }

      .wave.-three {
        animation: drift 5000ms infinite linear;
        z-index: 2 !important;
        opacity: 0.2;
      }

      .wave.-two {
        animation: drift 7000ms infinite linear;
        opacity: 0.1;
        z-index: 3 !important;
      }

      .box:after {
        content: "";
        display: block;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        z-index: 11;
        transform: translate3d(0, 0, 0);
      }

      @keyframes drift {
        from {
          transform: rotate(0deg);
        }
        from {
          transform: rotate(360deg);
        }
      }
      .info {
        position: absolute;
        bottom: 0;
        width: 100%;
        height: 45%;
        z-index: 4;
      }

      .location {
        margin-top: 1.5rem;
        text-align: center;
        font-weight: 800;
        font-size: 3rem;
      }

      .fa-street-view {
        animation: rotates 3s linear infinite alternate;
      }

      @keyframes rotates {
        from {
          transform: translateX(-0.5rem);
        }
        to {
          transform: translateX(0.5rem);
        }
      }

      #date {
        text-align: center;
        margin-top: 0.5rem;
        color: #57606f;
        font-size: 1.2rem;
        font-weight: 300;
        text-transform: uppercase;
      }

      .temp {
        margin-top: 2.5rem;
        text-align: center;
        font-size: 3rem;
      }

      .tempmin_max {
        text-align: center;
        margin-top: 0.3rem;
        font-weight: 300;
        font-size: 1.2rem;
        color: #57606f;
      }

      #weathercon {
        height: 55%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 3em;
      }

      #weathercon .fas {
        font-size: 6rem;
        animation: fas-anime 3s linear infinite alternate;
      }

      @keyframes fas-anime {
        from {
          transform: scale(1.1);
        }
        to {
          transform: scale(1.5);
        }
      }

      @media (max-width: 600px) {
        .box {
          width: 90vw;
          height: 80vh;
        }

        .wave {
          top: 85%;
        }

        #weathercon {
          font-size: 5em;
        }

        .info {
          font-size: 1.5rem;
        }
      }
      @media (max-height: 500px) {
        .box {
          height: 80vh;
        }

        .wave {
          top: 115%;
        }
      }
      body > span {
        width: 100vw;
        text-align: center;
        color: grey;
      }
    </style>
    <title>Weather App</title>
  </head>
  <body>
    <div class="box">
      <div class="wave -one"></div>
      <div class="wave -two"></div>
      <div class="wave -three"></div>

      <div id="weathercon">
        <i class="fas fa-sun" style="color: #eccc68"></i>
      </div>

      <div class="info">
        <h2 class="location"><i class="fa-solid fa-street-view"></i>Pune, In</h2>
        <p id="date">WED | OCT 23 | 10:49AM</p>
        <h1 class="temp">26.49°C</h1>
        <h3 class="tempmin_max">Min 26.49°C | Max 26.49°C </h3>
    </div>
      </div>
    </div>

    <script>
      const curDate = document.getElementById("date");
      let weathercon = document.getElementById("weathercon");

      const tempStatus = "{%tempstatus%}";

      //condition to check sunny or cloudy
      if (tempStatus == "Sunny") {
        weathercon.innerHTML =
          "<i class='fas  fa-sun' style='color: #eccc68;'></i>";
      } else if (tempStatus == "Clouds") {
        weathercon.innerHTML =
          "<i class='fas  fa-cloud' style='color: #f1f2f6;'></i>";
      } else if (tempStatus == "Rainy") {
        weathercon.innerHTML =
          "<i class='fas  fa-cloud-rain' style='color: #a4b0be;'></i>";
      } else {
        weathercon.innerHTML =
          "<i class='fas  fa-cloud' style='color:#f1f2f6;'></i>";
      }

      const getCurrentDay = () => {
        var weekday = new Array(7);
        weekday[0] = "Sunday";
        weekday[1] = "Monday";
        weekday[2] = "Tue";
        weekday[3] = "Wed";
        weekday[4] = "Thursday";
        weekday[5] = "Friday";
        weekday[6] = "Saturday";

        let currentTime = new Date();
        let day = weekday[currentTime.getDay()];
        return day;
      };

      const getCurrentTime = () => {
        var months = [
          "Jan",
          "Feb",
          "Mar",
          "Apr",
          "May",
          "June",
          "July",
          "Aug",
          "Sept",
          "Oct",
          "Nov",
          "Dec",
        ];

        var now = new Date();
        var month = months[now.getMonth() + 1];
        var date = now.getDate();

        let hours = now.getHours();
        let mins = now.getMinutes();

        let periods = "AM";

        if (hours > 11) {
          periods = "PM";
          if (hours > 12) hours -= 12;
        }
        if (mins < 10) {
          mins = "0" + mins;
        }

        return `${month} ${date} | ${hours}:${mins}${periods}`;
      };

      curDate.innerHTML = getCurrentDay() + " | " + getCurrentTime();
    </script>
  </body>
</html>