<!DOCTYPE html>
<html lang="en" >

<head>

  <meta charset="UTF-8">
  
<link rel="apple-touch-icon" type="image/png" href="https://cpwebassets.codepen.io/assets/favicon/apple-touch-icon-5ae1a0698dcc2402e9712f7d01ed509a57814f994c660df9f7a952f3060705ee.png" />
<meta name="apple-mobile-web-app-title" content="CodePen">

<link rel="shortcut icon" type="image/x-icon" href="https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico" />

<link rel="mask-icon" type="" href="https://cpwebassets.codepen.io/assets/favicon/logo-pin-8f3771b1072e3c38bd662872f6b673a722f4b3ca2421637d5596661b4e2132cc.svg" color="#111" />


  <title>CodePen - Task Complete Confetti Celebration</title>
  
  
  
  
<style>
* {
  box-sizing: border-box;
}

body, html {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  background-color: #FFFFFF;
  font-family: Arial;
}

.task {
  padding: 30px;
  width: 300px;
  background-color: #fff;
  box-shadow: 0 5px 30px rgba(255,255,255,255);
  border-radius: 2px;
}
.task + .task {
  margin-top: 10px;
}

.checkbox {
  position: relative;
  float: left;
  width: 20px;
  height: 20px;
  margin-right: 20px;
  border-radius: 50%;
  border: 2px solid #E5EEF9;
  transition: all 0.25s cubic-bezier(0, 0, 0, 1);
  cursor: pointer;
}
.checkbox.checked {
  background-color: #77DDA8;
  border: none;
}
.checkbox:active {
  transform: scale(0.8);
}
</style>

  <script>
  window.console = window.console || function(t) {};
</script>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/prefixfree/1.0.7/prefixfree.min.js"></script>

  
  <script>
  if (document.location.search.match(/type=embed/gi)) {
    window.parent.postMessage("resize", "*");
  }
</script>


</head>

<body translate="no" >
  <div class="task">
  <div class="checkbox"></div>
  <div class="description">Unleash the confetti</div>
</div>
    <script src="https://cpwebassets.codepen.io/assets/common/stopExecutionOnTimeout-8216c69d01441f36c0ea791ae2d4469f0f8ff5326f00ae2d00e4bb7d20e24edb.js"></script>

  
      <script id="rendered-js" >
var ran = function (min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
};

var Confetti = {
  active: false,
  amount: 10,
  colors: ['#FF8E70', '#C76DFC', '#4192F6', '#77DDA8', '#F8E71C'],
  newPiece: function () {
    var n = document.createElement('div');
    n.style.width = 4 + 'px';
    n.style.height = 6 + 'px';
    n.style.position = 'absolute';
    n.style.left = 0;
    n.style.right = 0;
    n.style.margin = '0 auto';
    n.style.opacity = 0;
    n.style.pointerEvents = 'none';
    n.style.backgroundColor = this.colors[ran(0, 4)];
    return n;
  },
  render: function (event) {
    var el = event.target;
    var c = Confetti.newPiece();
    var s = Confetti.size;
    var degs = 0;
    var x = 0;
    var y = 0;
    var opacity = 0;
    var count = 0;
    var xfactor;
    var yfactor = ran(10, 40) * (1 + s / 10);
    if (ran(0, 1) === 1) {
      xfactor = ran(5, 40) * (1 + s / 10);
      c.style.left = '-30px';
    } else
    {
      xfactor = ran(-5, -40) * (1 + s / 10);
      c.style.left = '30px';
    }
    var start = null;
    el.appendChild(c);
    var animate = function (timestamp) {
      if (!start) {start = timestamp;}
      var progress = timestamp - start;
      if (progress < 2000) {
        window.requestAnimationFrame(animate);
      } else
      {
        el.removeChild(c);
      }
      c.style.opacity = opacity;
      c.style.webkitTransform = 'translate3d(' + Math.cos(Math.PI / 36 * x) * xfactor + 'px, ' + Math.cos(Math.PI / 18 * y) * yfactor + 'px, 0) rotateZ(' + degs + 'deg) rotateY(' + degs + 'deg)';
      degs += 15;
      x += 0.5;
      y += 0.5;
      if (count > 25) {
        opacity -= 0.1;
      } else
      {
        opacity += 0.1;
      }
      count++;
    };
    window.requestAnimationFrame(animate);
  },
  fire: function (event) {
    if (event.target.classList.length === 1) {
      event.target.classList.add('checked');
      var count = 0;
      var launch = setInterval(function () {
        if (count < Confetti.amount) {
          Confetti.render(event);
          count++;
        } else
        {
          clearTimeout(launch);
        }
      }, 32);
      Confetti.active = true;
    } else
    {
      event.target.classList.remove('checked');
      Confetti.active = false;
    }
  },
  bindEvents: function () {
    var elements = document.querySelectorAll(this.element);
    for (var i = 0; i < elements.length; i++) {
      elements[i].onclick = Confetti.fire;
    }
  },
  init: function (el, amt, size) {
    this.element = el;
    this.amount = amt;
    this.size = size;
    this.bindEvents();
  } };


Confetti.init('.checkbox', 25, 1);
//# sourceURL=pen.js
    </script>

  

</body>

</html>
 
