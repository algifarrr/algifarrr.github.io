<!DOCTYPE html>
<html lang="en" >
<head>
  <meta charset="UTF-8">
  <title>hehe</title>
  <iframe src="https://www.youtube.com/embed/Kk60F8a7-Jw?autoplay=1&loops=1" width="0" height="0" frameborder="0"></iframe>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css">
  <style>
  @import 'https://fonts.googleapis.com/css?family=Roboto+Mono:100';
html,
body {
  font-family: 'Roboto Mono', monospace;
  background:-moz-linear-gradient(90deg, rgba(255,166,254,1) 0%, rgba(179,249,255,1) 100%); /* ff3.6+ */
background: -webkit-gradient(linear, left top, left bottom, color-stop(0%, rgba(179,249,255,1)), color-stop(100%, rgba(255,166,254,1))); /* safari4+,chrome */
background: -webkit-linear-gradient(90deg, rgba(255,166,254,1) 0%, rgba(179,249,255,1) 100%); /* safari5.1+,chrome10+ */
background: -o-linear-gradient(90deg, rgba(255,166,254,1) 0%, rgba(179,249,255,1) 100%); /* opera 11.10+ */
background: -ms-linear-gradient(90deg, rgba(255,166,254,1) 0%, rgba(179,249,255,1) 100%); /* ie10+ */
background: linear-gradient(0deg, rgba(255,166,254,1) 0%, rgba(179,249,255,1) 100%); /* w3c */
filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#B3F9FF', endColorstr='#FFA6FE',GradientType=0 ); /* ie6-9 */;
  height: 100%;
}
.container {
  height: 90%;
  width: 100%;
  justify-content: center;
  align-items: center;
  display: flex;
}
.text {
  font-weight: 100;
  font-size: 28px;
  color: #000000;
}
.dud {
  color: #757575;
}

</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/prefixfree/1.0.7/prefixfree.min.js"></script>

</head>
<body>
<div class="container">
  <div class="text"></div>
</div>  
  <script>// ——————————————————————————————————————————————————
    // TextScramble
    // ——————————————————————————————————————————————————
    
    class TextScramble {
      constructor(el) {
        this.el = el;
        this.chars = '!<>-_\\/[]{}—=+*^?#________';
        this.update = this.update.bind(this);
      }
      setText(newText) {
        const oldText = this.el.innerText;
        const length = Math.max(oldText.length, newText.length);
        const promise = new Promise(resolve => this.resolve = resolve);
        this.queue = [];
        for (let i = 0; i < length; i++) {
          const from = oldText[i] || '';
          const to = newText[i] || '';
          const start = Math.floor(Math.random() * 40);
          const end = start + Math.floor(Math.random() * 40);
          this.queue.push({ from, to, start, end });
        }
        cancelAnimationFrame(this.frameRequest);
        this.frame = 0;
        this.update();
        return promise;
      }
      update() {
        let output = '';
        let complete = 0;
        for (let i = 0, n = this.queue.length; i < n; i++) {
          let { from, to, start, end, char } = this.queue[i];
          if (this.frame >= end) {
            complete++;
            output += to;
          } else if (this.frame >= start) {
            if (!char || Math.random() < 0.75) {
              char = this.randomChar();
              this.queue[i].char = char;
            }
            output += `<span class="dud">${char}</span>`;
          } else {
            output += from;
          }
        }
        this.el.innerHTML = output;
        if (complete === this.queue.length) {
          this.resolve();
        } else {
          this.frameRequest = requestAnimationFrame(this.update);
          this.frame++;
        }
      }
      randomChar() {
        return this.chars[Math.floor(Math.random() * this.chars.length)];
      }}
    
    
    // ——————————————————————————————————————————————————
    // Example
    // ——————————————————————————————————————————————————
    
    const phrases = [
    'Selamat sore dedek Arum...',
    'jangan lupa Bahagia >_<.',
    ];
    
    
    const el = document.querySelector('.text');
    const fx = new TextScramble(el);
    
    let counter = 0;
    const next = () => {
      fx.setText(phrases[counter]).then(() => {
        setTimeout(next, 2000);
      });
      counter = (counter + 1) % phrases.length;
    };
    
    next();</script>

</body>
</html>

