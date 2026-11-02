<!DOCTYPE html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover"><meta name="mobile-web-app-capable" content="yes"><meta name="apple-mobile-web-app-capable" content="yes"><meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"><meta name="theme-color" content="#000000"><title>Dz Saga</title><style>
html,body{height:100%;margin:0;background:#000;color:#fff;font-family:monospace;overflow:hidden;touch-action:none;user-select:none;-webkit-user-select:none;-webkit-tap-highlight-color:transparent}
#app,#wrap{direction:ltr}#app{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;padding:env(safe-area-inset-top) env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left);box-sizing:border-box}
#wrap{position:relative;width:min(100%,calc((100vh - env(safe-area-inset-top) - env(safe-area-inset-bottom))*1.8182));aspect-ratio:640/352}
canvas{width:100%;height:100%;display:block;image-rendering:auto;background:#000;filter:saturate(1.16) contrast(1.05)}
#top{position:absolute;top:1.5%;right:1.2%;display:flex;gap:5px}
#top b{width:30px;height:30px;border-radius:8px;background:#0007;border:1px solid #fff5;display:flex;align-items:center;justify-content:center;font-size:15px}
#pad{position:absolute;left:0;right:0;bottom:4%;display:flex;justify-content:space-between;padding:0 3%;pointer-events:none}
#pad div{display:flex;gap:14px}
#pad b{pointer-events:auto;width:62px;height:62px;border-radius:50%;background:#fff3;border:2px solid #fff7;display:flex;align-items:center;justify-content:center;font-size:24px}
.ov{position:absolute;inset:0;display:none;flex-direction:column;align-items:center;justify-content:center;gap:6px;background:#000b;padding:6px;box-sizing:border-box;overflow:auto;font-size:clamp(11px,2.3vmin,15px)}
#m{display:flex;background:#0006}
#m h1{margin:0;font-size:clamp(16px,5vmin,34px);color:#ffd84a;text-shadow:3px 3px #b3261e;text-align:center}
.row{display:flex;flex-wrap:wrap;justify-content:center;gap:5px}
button{font:bold 1em monospace;padding:.45em 1em;border:2px solid #fff;background:#c0392b;color:#fff;border-radius:6px}
button.on{background:#27ae60}button:disabled{opacity:.35}
.row button[data-l],.row button[data-c]{background:#2c3e50;font-size:.85em;padding:.3em .7em}
.row button[data-d]{background:#7f3b8a}.row button[data-d].on{background:#27ae60}
.ds{font-size:.9em;color:#ffd84a;text-align:center;min-height:1.2em}
#sh .r{display:flex;align-items:center;gap:10px;width:92%;max-width:520px;background:#1e2a3a;border:2px solid #fff6;border-radius:8px;padding:5px;box-sizing:border-box}
#sh img{width:48px;height:48px;border-radius:6px;object-fit:cover}#sh .t{flex:1}
#rot{display:none}
@media (orientation:portrait){#app{align-items:flex-start}#wrap{width:100%}#pad{position:fixed;bottom:5%}#rot{display:block;position:fixed;bottom:22%;left:0;right:0;text-align:center;color:#ffd84a;font-size:13px}}
</style></head><body><div id="app"><div id="wrap"><canvas id="c" width="640" height="352"></canvas>
<div id="top"><b id="ps">⏸</b><b id="sp">🛒</b><b id="mu">🔊</b><b id="fsb">⛶</b></div>
<div id="pad"><div><b data-k="l">◀</b><b data-k="r">▶</b></div><div><b data-k="j">A</b></div></div>
<div id="m" class="ov"></div><div id="sh" class="ov"></div><div id="pz" class="ov"></div></div><div id="rot"></div></div>
<script>
const C=document.getElementById('c');let X=C.getContext('2d');
const W=640,H=352,T=32,R=11,$=id=>document.getElementById(id);
let t=0,cam=0,age=0,lang='ar',diff=0,ch=0,lvl=0,state='menu',paused=false,own={},coins=0,score=0,tmr=0,itm=0,sl=0,SL=[],nxt=0,dlg=null,shk=0,mute=false,AC,L=null,p=null,lastSafe=null,PT=[],PR=[],K={l:0,r:0,j:0},SV={lvl:0,max:0,coins:0,diff:0};
const rc=(c,a,b,w,h)=>{X.fillStyle=c;X.fillRect(Math.round(a),Math.round(b),w,h)};
const hs=n=>{n=Math.imul(n^n>>>13,1274126177);return((n^n>>>16)>>>0)%1000};
