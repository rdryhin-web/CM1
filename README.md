<!DOCTYPE html>
<html lang="ru"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, user-scalable=no">
<title>Дюна-7: закладка бомбы</title>
<style>
:root{--ink:#f3e6cf;--acc:#e8a33d;--hp:#7fc27a;--bad:#d9553b;color-scheme:dark}
*{box-sizing:border-box;-webkit-user-select:none;user-select:none;-webkit-touch-callout:none;-webkit-tap-highlight-color:transparent}
html,body{margin:0;height:100%;background:#1b1713;color:var(--ink);font-family:"Trebuchet MS",Verdana,sans-serif;overflow:hidden;touch-action:none}
canvas{position:fixed;inset:0;width:100%;height:100%}
body:after{content:'';position:fixed;inset:0;pointer-events:none;box-shadow:inset 0 0 140px #0007}
#look{position:fixed;inset:0}
.h{position:fixed;pointer-events:none;font-weight:700;text-shadow:0 1px 3px #000}
#hp{left:calc(12px + env(safe-area-inset-left,0px));top:calc(34px + env(safe-area-inset-top,0px));font-size:20px;color:var(--hp)}
#mon{left:calc(12px + env(safe-area-inset-left,0px));top:calc(60px + env(safe-area-inset-top,0px));font-size:20px;color:var(--acc)}
#top{left:0;right:0;top:calc(8px + env(safe-area-inset-top,0px));text-align:center;font-size:17px}
#ammo{right:calc(22px + env(safe-area-inset-right,0px));bottom:calc(245px + env(safe-area-inset-bottom,0px));font-size:22px}
#feed{right:calc(12px + env(safe-area-inset-right,0px));top:calc(34px + env(safe-area-inset-top,0px));font-size:14px;text-align:right}
#msg{left:0;right:0;top:28%;text-align:center;font-size:24px;color:var(--acc)}
#cross{left:50%;top:50%;width:18px;height:18px;margin:-9px 0 0 -9px}
#cross:before,#cross:after{content:"";position:absolute;background:var(--ink)}
#cross:before{left:8px;width:2px;height:18px}#cross:after{top:8px;height:2px;width:18px}
#flash{position:fixed;inset:0;background:radial-gradient(transparent 40%,var(--bad));opacity:0;pointer-events:none;transition:opacity .25s}
#stick{position:fixed;left:calc(22px + env(safe-area-inset-left,0px));bottom:calc(26px + env(safe-area-inset-bottom,0px));width:130px;height:130px;border-radius:50%;border:2px solid #f3e6cf55;background:#0004}
#knob{position:absolute;left:41px;top:41px;width:48px;height:48px;border-radius:50%;background:#f3e6cf99}
.b{position:fixed;border-radius:50%;border:2px solid #f3e6cf88;background:#e8a33d66;color:var(--ink);font-weight:700;display:flex;align-items:center;justify-content:center;text-align:center;font-size:13px}
#fire{right:calc(24px + env(safe-area-inset-right,0px));bottom:calc(40px + env(safe-area-inset-bottom,0px));width:104px;height:104px;font-size:18px}
#rel{right:calc(142px + env(safe-area-inset-right,0px));bottom:calc(30px + env(safe-area-inset-bottom,0px));width:62px;height:62px;background:#0005}
#sw{right:calc(150px + env(safe-area-inset-right,0px));bottom:calc(100px + env(safe-area-inset-bottom,0px));width:56px;height:56px;background:#0005}
#act{left:50%;bottom:calc(150px + env(safe-area-inset-bottom,0px));margin-left:-48px;width:96px;height:96px;background:#d9553b99;display:none}
#shopBtn{left:calc(12px + env(safe-area-inset-left,0px));top:calc(90px + env(safe-area-inset-top,0px));width:74px;height:44px;border-radius:10px;background:#e8a33d99;display:none}
#shop{position:fixed;inset:0;background:#1b1713f2;z-index:4;display:none;padding:calc(12px + env(safe-area-inset-top,0px)) 14px 14px;overflow:auto}
#shop h2{margin:0 0 8px;color:var(--acc);font-size:20px}
#grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.it{padding:10px;border-radius:10px;background:#3a3126;border:1px solid #f3e6cf33;font-size:14px;line-height:1.3}
.it b{color:var(--acc)}
#close{margin-top:12px;font:700 18px inherit;padding:12px 30px;border:0;border-radius:10px;background:var(--acc);color:#1b1713}
#chat{position:fixed;left:calc(12px + env(safe-area-inset-left,0px));top:calc(130px + env(safe-area-inset-top,0px));width:62%;font-size:13px;text-shadow:0 1px 2px #000;line-height:1.25}#chat div{margin-bottom:2px}#white{position:fixed;inset:0;background:#fff;opacity:0;pointer-events:none;z-index:3}#gr{right:calc(24px + env(safe-area-inset-right,0px));bottom:calc(158px + env(safe-area-inset-bottom,0px));width:60px;height:60px;background:#0005}#grs{right:calc(92px + env(safe-area-inset-right,0px));bottom:calc(170px + env(safe-area-inset-bottom,0px));width:54px;height:54px;background:#0005;font-size:10px}
#start{position:fixed;inset:0;background:#1b1713ee;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:24px;z-index:5}
#start h1{font-size:40px;margin:0 0 8px;color:var(--acc)}
#start p{max-width:340px;line-height:1.45;margin:0 0 18px;color:#d8c8ab}
#go{font:700 20px "Trebuchet MS",Verdana,sans-serif;padding:14px 38px;border:0;border-radius:10px;background:var(--acc);color:#1b1713}
</style></head><body>
<div id="look"></div><div class="h" id="cross"></div><div id="flash"></div>
<div class="h" id="hp"></div><div class="h" id="mon"></div><div class="h" id="top"></div>
<div class="h" id="ammo"></div><div class="h" id="feed"></div><div class="h" id="msg"></div>
<div id="stick"><div id="knob"></div></div>
<div class="b" id="rel">Заряд</div><div class="b" id="sw">Смена</div><div class="b" id="fire">Огонь</div>
<div class="b" id="act"></div><div class="b" id="gr">Бросок</div><div class="b" id="grs"></div><div class="b" id="shopBtn">Магазин</div>
<div class="h" id="chat"></div><div id="white"></div><div id="shop"><h2 id="sh">Магазин</h2><div id="grid"></div><button id="close">Закрыть</button></div>
<div id="start"><h1>Дюна-7</h1>
<p>Закладка бомбы, 10 раундов, 5 на 5. Вы начинаете за террористов: заложите бомбу на точке A или B. После пятого раунда стороны меняются. Старт: 800 $.</p>
<button id="go">Играть</button></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
const $=id=>document.getElementById(id),R=Math.random;
const renderer=new THREE.WebGLRenderer({antialias:true});renderer.setPixelRatio(Math.min(devicePixelRatio,2));
renderer.shadowMap.enabled=true;renderer.shadowMap.type=THREE.PCFSoftShadowMap;
renderer.toneMapping=THREE.ACESFilmicToneMapping;renderer.toneMappingExposure=1.25;renderer.outputEncoding=THREE.sRGBEncoding;document.body.prepend(renderer.domElement);
const scene=new THREE.Scene();
const skyC=document.createElement('canvas');skyC.width=2;skyC.height=256;{const x=skyC.getContext('2d'),g=x.createLinearGradient(0,0,0,256);g.addColorStop(0,'#5b8fc9');g.addColorStop(.55,'#a9c6dc');g.addColorStop(1,'#e6cfa0');x.fillStyle=g;x.fillRect(0,0,2,256)}
const skyT=new THREE.CanvasTexture(skyC);skyT.encoding=THREE.sRGBEncoding;scene.background=skyT;scene.fog=new THREE.Fog(0xd9b98a,35,140);
const glowC=document.createElement('canvas');glowC.width=glowC.height=128;{const x=glowC.getContext('2d'),g=x.createRadialGradient(64,64,0,64,64,64);g.addColorStop(0,'rgba(255,245,210,1)');g.addColorStop(.2,'rgba(255,220,150,.5)');g.addColorStop(1,'rgba(255,200,120,0)');x.fillStyle=g;x.fillRect(0,0,128,128)}
const sunS=new THREE.Sprite(new THREE.SpriteMaterial({map:new THREE.CanvasTexture(glowC),blending:THREE.AdditiveBlending,depthWrite:false,fog:false}));sunS.scale.set(140,140,1);sunS.position.set(100,90,-120);scene.add(sunS);
const cam=new THREE.PerspectiveCamera(75,1,.1,220);cam.rotation.order='YXZ';scene.add(cam);
scene.add(new THREE.HemisphereLight(0xfff0d0,0x8a6a40,.6));
const sun=new THREE.DirectionalLight(0xfff1d6,1.2);sun.position.set(30,60,20);sun.castShadow=true;sun.shadow.mapSize.set(2048,2048);sun.shadow.bias=-.0005;
Object.assign(sun.shadow.camera,{left:-75,right:75,top:75,bottom:-75,far:220});scene.add(sun);
function resize(){renderer.setSize(innerWidth,innerHeight);cam.aspect=innerWidth/innerHeight;cam.updateProjectionMatrix()}addEventListener('resize',resize);resize();
function tex(base,rep,mortar){const c=document.createElement('canvas');c.width=c.height=256;const x=c.getContext('2d');x.fillStyle=base;x.fillRect(0,0,256,256);
for(let i=0;i<5000;i++){x.fillStyle=R()<.5?'rgba(0,0,0,.07)':'rgba(255,240,200,.07)';x.fillRect(R()*256,R()*256,2+R()*3,2+R()*3)}
if(mortar){x.strokeStyle='rgba(60,40,20,.35)';x.lineWidth=2;for(let y=0;y<256;y+=32){x.beginPath();x.moveTo(0,y);x.lineTo(256,y);x.stroke();for(let xx=(y/32%2)*32;xx<256;xx+=64){x.beginPath();x.moveTo(xx,y);x.lineTo(xx,y+32);x.stroke()}}}
const t=new THREE.CanvasTexture(c);t.wrapS=t.wrapT=THREE.RepeatWrapping;t.repeat.set(rep,rep);t.anisotropy=8;t.encoding=THREE.sRGBEncoding;return t}
const floor=new THREE.Mesh(new THREE.PlaneGeometry(100,120),(()=>{const t=tex('#c9a66b',28,0);return new THREE.MeshStandardMaterial({map:t,bumpMap:t,bumpScale:3,roughness:1})})());
floor.rotation.x=-Math.PI/2;floor.receiveShadow=true;scene.add(floor);
const wallM=(()=>{const t=tex('#b98f5a',3,1);return new THREE.MeshStandardMaterial({map:t,bumpMap:t,bumpScale:2.5,roughness:.95,vertexColors:true})})(),crateM=(()=>{const t=tex('#7a5430',1,0);return new THREE.MeshStandardMaterial({map:t,bumpMap:t,bumpScale:1.5,roughness:.8,vertexColors:true})})();
const boxes=[],capM=new THREE.MeshStandardMaterial({color:0x8a6a3e,roughness:.9});
function aoGeo(w,h,d){const g=new THREE.BoxGeometry(w,h,d),p=g.attributes.position,c=[];for(let i=0;i<p.count;i++){const k=.55+.45*Math.min(1,(p.getY(i)+h/2)/2.2);c.push(k,k,k)}g.setAttribute('color',new THREE.Float32BufferAttribute(c,3));return g}
function addBox(cx,cz,w,d,h,mat){const m=new THREE.Mesh(aoGeo(w,h,d),mat||wallM);m.position.set(cx,h/2,cz);m.castShadow=m.receiveShadow=true;scene.add(m);if(h>=5){const c=new THREE.Mesh(new THREE.BoxGeometry(w+.5,.5,d+.5),capM);c.position.set(cx,h+.25,cz);c.castShadow=true;scene.add(c)}boxes.push({x0:cx-w/2,x1:cx+w/2,y0:0,y1:h,z0:cz-d/2,z1:cz+d/2})}
function addY(cx,cy,cz,w,h,d){const m=new THREE.Mesh(aoGeo(w,h,d),wallM);m.position.set(cx,cy,cz);m.castShadow=true;scene.add(m);boxes.push({x0:cx-w/2,x1:cx+w/2,y0:cy-h/2,y1:cy+h/2,z0:cz-d/2,z1:cz+d/2})}
[[0,-60,100,2,9],[0,60,100,2,9],[-50,0,2,120,9],[50,0,2,120,9],[32,8,2,56,6],[9,10,2,46,6],[-9,10,2,46,6],[-32,8,2,56,6],[-41,14,2,28,6],[-24,42,30,2,6],[24,42,30,2,6],[20,-28,2,16,6],[-20,-28,2,16,6],[0,-36,16,2,6],[20,5,10,14,6],[-20,5,10,14,6],[14,-14,2,2,4],[-14,-14,2,2,4],[0,-16,1.5,1.5,3],[41,-22,12,2,5],[-41,-22,12,2,5]].forEach(b=>addBox(...b));
addY(0,6,-14,18,2,2);addY(44.5,6,40,11,2,2);addY(-44.5,6,40,11,2,2);
[[34,-44,3,3,2],[46,-46,3,3,2.5],[40,-52,4,3,1.5],[43,-30,3,3,3],[36,-30,3,3,1.5],[46,-36,2,2,2],[0,-6,3,3,1.5],[0,12,4,2,2],[0,28,3,3,1.5],[28,18,3,3,2],[28,-4,3,3,1.5],[41,30,3,3,2],[44,10,2,2,1.5],[20,50,3,2,1.5],[-20,50,3,2,1.5],[0,46,2,2,2.5],[-15,-52,3,3,2],[15,-52,3,3,2],
[-34,-44,3,3,2],[-46,-46,3,3,2.5],[-40,-52,4,3,1.5],[-43,-30,3,3,3],[-36,-30,3,3,1.5],[-46,-36,2,2,2],[-28,18,3,3,2],[-28,-4,3,3,1.5],[-46,36,3,3,2],[-46,10,2,2,1.5]].forEach(b=>addBox(...b,crateM));
{const im=new THREE.InstancedMesh(new THREE.DodecahedronGeometry(.18,0),new THREE.MeshStandardMaterial({color:0x9c8458,roughness:1}),220),mm=new THREE.Matrix4(),q=new THREE.Quaternion(),e=new THREE.Euler();let n=0;
for(let k=0;k<500&&n<220;k++){const x=(R()-.5)*96,z=(R()-.5)*116;if(hits(x,z,.6))continue;const sc=.4+R()*1.2;q.setFromEuler(e.set(R()*3,R()*3,R()*3));mm.compose(new THREE.Vector3(x,.05,z),q,new THREE.Vector3(sc,sc*.6,sc));im.setMatrixAt(n++,mm)}im.count=n;im.castShadow=im.receiveShadow=true;scene.add(im)}
const dustG=new THREE.BufferGeometry(),dp=[];for(let i=0;i<260;i++)dp.push((R()-.5)*50,R()*6,(R()-.5)*50);dustG.setAttribute('position',new THREE.Float32BufferAttribute(dp,3));
const dust=new THREE.Points(dustG,new THREE.PointsMaterial({color:0xfff0c8,size:.06,transparent:true,opacity:.5,depthWrite:false}));scene.add(dust);
const SITE=[[40,-40],[-40,-40]],HOLD=[[34,-33],[-34,-33],[0,-30]];
[0,1].forEach(i=>{const m=new THREE.Mesh(new THREE.CircleGeometry(6,32),new THREE.MeshBasicMaterial({color:0xe8a33d,transparent:true,opacity:.25}));m.rotation.x=-Math.PI/2;m.position.set(SITE[i][0],.03,SITE[i][1]);scene.add(m);
 const c=document.createElement('canvas');c.width=c.height=64;const x=c.getContext('2d');x.font='bold 56px sans-serif';x.fillStyle='#ffd27a';x.textAlign='center';x.fillText('AB'[i],32,50);
 const s=new THREE.Sprite(new THREE.SpriteMaterial({map:new THREE.CanvasTexture(c),transparent:true}));s.scale.set(3,3,1);s.position.set(SITE[i][0],4,SITE[i][1]);scene.add(s)});
const bombM=new THREE.Group();{const m=new THREE.MeshStandardMaterial({color:0x222222});const a=new THREE.Mesh(new THREE.BoxGeometry(.5,.25,.35),m);a.position.y=.13;bombM.add(a);const l=new THREE.Mesh(new THREE.BoxGeometry(.08,.08,.08),new THREE.MeshBasicMaterial({color:0xff2200}));l.position.y=.3;bombM.add(l)}bombM.visible=false;scene.add(bombM);

function rayBox(o,d,b,max){let a=0,z=max;const lo=[b.x0,b.y0,b.z0],hi=[b.x1,b.y1,b.z1],oo=[o.x,o.y,o.z],dd=[d.x,d.y,d.z];
for(let i=0;i<3;i++){if(Math.abs(dd[i])<1e-8){if(oo[i]<lo[i]||oo[i]>hi[i])return -1}else{let t1=(lo[i]-oo[i])/dd[i],t2=(hi[i]-oo[i])/dd[i];if(t1>t2){const s=t1;t1=t2;t2=s}a=Math.max(a,t1);z=Math.min(z,t2);if(a>z)return -1}}return a}
function wallDist(o,d,max){let m=max;for(const b of boxes){const t=rayBox(o,d,b,m);if(t>=0&&t<m)m=t}return m}
function hits(x,z,r){for(const b of boxes)if(b.y1>.9&&b.y0<1.7&&x>b.x0-r&&x<b.x1+r&&z>b.z0-r&&z<b.z1+r)return true;return false}
function move(p,dx,dz,r){if(!hits(p.x+dx,p.z,r))p.x+=dx;if(!hits(p.x,p.z+dz,r))p.z+=dz}
function bx(w,h,d,x,y,z,c,p,rx){const m=new THREE.Mesh(new THREE.BoxGeometry(w,h,d),new THREE.MeshStandardMaterial({color:c,roughness:.7,metalness:c<0x444444?.5:.05}));m.position.set(x,y,z);if(rx)m.rotation.x=rx;m.castShadow=true;p.add(m);return m}

// weapons
const W=[{n:'Пистолет',p:0,d:22,r:.2,m:12,rl:1.5,s:.015,pel:1,len:.6},{n:'ПП',p:1200,d:18,r:.075,m:30,rl:1.8,s:.035,pel:1,len:.8},{n:'Дробовик',p:1800,d:11,r:.85,m:6,rl:2.2,s:.07,pel:8,len:1},
{n:'Карабин',p:2700,d:26,r:.09,m:30,rl:2,s:.02,pel:1,len:1.1},{n:'Автомат',p:2700,d:33,r:.1,m:30,rl:2.2,s:.022,pel:1,len:1.2},{n:'Снайперка',p:4750,d:115,r:1.2,m:5,rl:2.6,s:.002,pel:1,len:1.5,sc:1},{n:'Пулемёт',p:5200,d:30,r:.08,m:100,rl:4,s:.04,pel:1,len:1.3}];
const gunH=new THREE.Group();gunH.position.set(.25,-.25,-.55);cam.add(gunH);let mf;
function mkGun(w){gunH.clear();const g=new THREE.Group(),i=W.indexOf(w),M=0x1e1e1e,D=0x2f2f2f,Wd=0x7a4a22,S=0xc99a76,B=(a,b,c,x,y,z,col,rx)=>bx(a,b,c,x,y,z,col,g,rx);
if(i===0){B(.04,.05,.2,0,.03,-.08,0x3a3a3a);B(.036,.04,.18,0,-.01,-.06,M);B(.04,.1,.05,0,-.07,.04,M,.2);B(.02,.012,.04,0,.06,-.17,D);B(.012,.02,.012,0,.065,0,D);B(.01,.03,.04,0,-.035,-.02,D)}
else if(i===1){B(.06,.08,.3,0,0,-.05,M);B(.045,.045,.2,0,.01,-.3,D);B(.035,.18,.05,0,-.13,-.08,M);B(.03,.03,.22,0,.01,.2,D);B(.05,.04,.04,0,-.02,.3,D);B(.03,.02,.28,0,.05,-.05,D)}
else if(i===2){B(.07,.09,.3,0,0,0,M);B(.03,.03,.6,0,.025,-.45,D);B(.034,.034,.5,0,-.02,-.4,D);B(.065,.05,.2,0,-.035,-.3,Wd);B(.05,.1,.3,0,-.03,.3,Wd,.1);B(.012,.02,.012,0,.05,-.74,0x111111)}
else if(i===3){B(.06,.07,.36,0,.02,-.04,D);B(.055,.055,.32,0,.01,-.36,M);B(.02,.02,.22,0,.015,-.62,M);B(.03,.03,.34,0,.075,-.04,M);B(.04,.17,.06,0,-.12,-.06,M,-.12);B(.05,.08,.28,0,-.02,.3,M);B(.01,.04,.01,0,.06,-.7,M)}
else if(i===4){B(.07,.09,.34,0,0,-.02,M);B(.06,.035,.3,0,.06,-.04,D);B(.062,.06,.22,0,-.01,-.28,Wd);B(.062,.03,.22,0,.04,-.28,Wd);B(.018,.018,.34,0,.045,-.48,0x151515);B(.022,.022,.34,0,.015,-.52,0x151515);B(.012,.05,.014,0,.06,-.66,0x151515);B(.04,.1,.07,0,-.12,-.07,M,-.15);B(.04,.1,.07,0,-.2,-.14,M,-.55);B(.05,.1,.26,0,-.03,.3,Wd,.1);B(.03,.03,.05,0,.015,-.7,0x151515)}
else if(i===5){B(.065,.09,.4,0,0,0,M);B(.022,.022,.9,0,.02,-.65,D);B(.05,.05,.3,0,.095,-.1,0x111111);B(.056,.056,.03,0,.095,-.26,0x335577);B(.056,.056,.03,0,.095,.06,0x335577);B(.03,.04,.05,0,.05,-.1,M);B(.05,.1,.34,0,-.03,.36,Wd,.1);B(.035,.07,.05,0,-.1,-.05,M);B(.012,.12,.012,.04,-.07,-.7,D,.4);B(.012,.12,.012,-.04,-.07,-.7,D,.4)}
else{B(.08,.1,.42,0,0,0,M);B(.03,.03,.85,0,.02,-.6,D);B(.045,.045,.4,0,.01,-.5,M);B(.12,.12,.16,0,-.13,-.02,0x3a4a2a);B(.03,.04,.3,0,.08,-.04,D);B(.012,.14,.012,.05,-.08,-.75,D,.5);B(.012,.14,.012,-.05,-.08,-.75,D,.5);B(.05,.1,.26,0,-.03,.3,M,.05)}
const fg=[-.08,-.2,-.3,-.35,-.28,-.4,-.45][i],mz=[-.25,-.5,-.85,-.8,-.85,-1.25,-1.1][i];B(.06,.06,.08,0,-.07,fg,S);B(.06,.06,.08,0,-.13,i?.08:.04,S);
mf=new THREE.Mesh(new THREE.PlaneGeometry(.28,.28),new THREE.MeshBasicMaterial({color:0xffc060,transparent:true,opacity:.9,blending:THREE.AdditiveBlending,depthWrite:false}));mf.position.set(0,.015,mz-.05);mf.visible=false;g.add(mf);gunH.add(g)}

// audio + fx
let AC;const sfx={init(){AC=new (window.AudioContext||window.webkitAudioContext)();const n=AC.sampleRate,b=AC.createBuffer(1,n,n),d=b.getChannelData(0);for(let i=0;i<n;i++)d[i]=R()*2-1;this.nb=b;this.m=AC.createGain();
const cp=AC.createDynamicsCompressor(),cv=AC.createConvolver(),il=Math.floor(n*1.2),ib=AC.createBuffer(2,il,n);for(let c=0;c<2;c++){const e=ib.getChannelData(c);for(let i=0;i<il;i++)e[i]=(R()*2-1)*Math.pow(1-i/il,3)}cv.buffer=ib;const wet=AC.createGain();wet.gain.value=.25;this.m.connect(cp);this.m.connect(cv);cv.connect(wet);wet.connect(cp);cp.connect(AC.destination)},
noise(dur,f,vol,type){if(!AC)return;const s=AC.createBufferSource();s.buffer=this.nb;const fl=AC.createBiquadFilter();fl.type=type||'lowpass';fl.frequency.value=f;const g=AC.createGain(),t=AC.currentTime;g.gain.setValueAtTime(vol,t);g.gain.exponentialRampToValueAtTime(.001,t+dur);s.connect(fl);fl.connect(g);g.connect(this.m);s.start(t);s.stop(t+dur)},
tone(f,dur,vol,type,f2){if(!AC)return;const o=AC.createOscillator(),g=AC.createGain(),t=AC.currentTime;o.type=type||'sine';o.frequency.setValueAtTime(f,t);if(f2)o.frequency.exponentialRampToValueAtTime(f2,t+dur);g.gain.setValueAtTime(vol,t);g.gain.exponentialRampToValueAtTime(.001,t+dur);o.connect(g);g.connect(this.m);o.start(t);o.stop(t+dur)},
shot(v,p){v=v||1;const r=(.85+R()*.3)*(p||1);this.noise(.05,9000*r,.7*v,'highpass');this.noise(.15,2500*r,.9*v,'bandpass');this.noise(.45,450*r,.9*v);this.tone(150*r,.22,.8*v,'sine',38)},
click(){this.noise(.04,4000,.35,'highpass');this.tone(300,.05,.15,'square')},hit(){this.tone(1500,.07,.25,'square')},hurt(){this.tone(110,.3,.5,'sawtooth',45)},beep(){this.tone(1800,.08,.3,'square')},
boom(){this.noise(1.2,300,1.6);this.tone(70,1,1.4,'sine',20)},buy(){this.tone(900,.08,.25,'triangle');setTimeout(()=>this.tone(1300,.08,.25,'triangle'),80)}};
const fx=[];
function puff(p,n,col){for(let i=0;i<n;i++){const m=new THREE.Mesh(new THREE.BoxGeometry(.06,.06,.06),new THREE.MeshBasicMaterial({color:col,transparent:true}));m.position.copy(p);scene.add(m);fx.push({m,v:new THREE.Vector3((R()-.5)*3,R()*3,(R()-.5)*3),l:.5})}}
function tracer(a,b){const l=new THREE.Line(new THREE.BufferGeometry().setFromPoints([a.clone(),b.clone()]),new THREE.LineBasicMaterial({color:0xffe9a0,transparent:true}));scene.add(l);fx.push({m:l,l:.08,line:1})}
function fxUpdate(dt){for(let i=fx.length-1;i>=0;i--){const f=fx[i];f.l-=dt;if(f.l<=0){scene.remove(f.m);f.m.geometry.dispose();f.m.material.dispose();fx.splice(i,1);continue}
if(f.line)f.m.material.opacity=f.l/.08;else{f.v.y-=9*dt;f.m.position.addScaledVector(f.v,dt);f.m.material.opacity=f.l*2}}}

// state
const G={round:0,ph:'buy',t:0,sc:[0,0],loss:[0,0],bomb:{on:0},over:0,NZ:[],nz:[]};
const P={x:0,z:44,yaw:0,pitch:0,hp:100,arm:0,kit:0,money:800,team:0,alive:true,pri:0,cur:0,ammo:{0:12},reload:0,cool:0,kills:0,act:0,name:'Вы',gr:{flash:0,smoke:0,he:0,mol:0},gsel:null};
const NT=['Тайфун','Вольт','Ястреб','Скиба'],NE=['Рейдер','Кобра','Фантом','Гром','Дымок'];
const bots=[];
function label(txt,col,thru){const c=document.createElement('canvas');c.width=256;c.height=64;const x=c.getContext('2d');x.font='bold 34px Trebuchet MS';x.textAlign='center';x.shadowColor=col;x.shadowBlur=14;x.fillStyle=col;x.fillText(txt,128,42);
const s=new THREE.Sprite(new THREE.SpriteMaterial({map:new THREE.CanvasTexture(c),transparent:true,depthTest:!thru}));s.scale.set(1.6,.4,1);s.position.y=2.3;s.renderOrder=9;return s}
function skin(b){if(b.g){ragEnd(b);scene.remove(b.g)}const g=new THREE.Group(),pal=b.team?[0x2d3a52,0x1c2433,0x4a5a78]:[0x6b5a3e,0x3a3226,0x8a7855];
b.legs=[-1,1].map(s=>{const l=new THREE.Group();l.position.set(s*.13,.9,0);g.add(l);bx(.2,.45,.24,0,-.22,0,pal[0],l);const k=new THREE.Group();k.position.set(0,-.45,0);l.add(k);bx(.18,.45,.2,0,-.22,0,pal[1],k);bx(.22,.12,.34,0,-.45,.05,0x151515,k);l.userData.k=k;return l});
const tor=new THREE.Group();tor.position.y=1.2;g.add(tor);b.tor=tor;bx(.5,.3,.28,0,-.25,0,pal[0],tor);bx(.56,.6,.32,0,.1,0,pal[0],tor);bx(.5,.46,.14,0,.1,.2,pal[1],tor);[-.17,0,.17].forEach(x=>bx(.12,.14,.08,x,-.1,.28,pal[2],tor));
const hd=new THREE.Group();hd.position.y=1.75;g.add(hd);b.hd=hd;bx(.22,.22,.22,0,-.05,0,0x1a1a1a,hd);bx(.3,.13,.32,0,.08,0,pal[1],hd);bx(.24,.06,.05,0,-.03,.12,0x4a6a80,hd);
const rf=new THREE.Group();rf.position.set(.05,1.25,.2);g.add(rf);b.rifle=rf;
bx(.07,.09,.55,0,0,.3,0x222222,rf);bx(.07,.07,.25,0,0,.68,0x6b4423,rf);bx(.04,.04,.35,0,.01,.98,0x151515,rf);b.mag=bx(.05,.2,.08,0,-.14,.28,0x222222,rf,-.3);bx(.05,.1,.2,0,-.03,-.05,0x6b4423,rf);
bx(.1,.1,.5,-.1,-.07,.45,pal[0],rf);bx(.1,.1,.3,.14,-.07,.1,pal[0],rf);bx(.08,.08,.08,-.1,-.07,.72,0xc99a76,rf);
b.lab=label(b.name,b.team===P.team?'#6fe3ff':'#ff6a4a',b.team===P.team);g.add(b.lab);scene.add(g);b.g=g}
for(let i=0;i<9;i++){const b={name:i<4?NT[i]:NE[i-4],team:i<4?0:1,x:0,z:0,hp:100,arm:0,kit:0,money:800,w:0,ammo:12,alive:true,rl:0,cd:1,sp:0,st:0,burst:0,react:0,kick:0,lt:0,ph:0,t:0,sd:R()<.5?1:-1,act:0,site:0,gx:0,gz:0};bots.push(b);skin(b)}
const mates=t=>[...bots.filter(b=>b.team===t),...(P.team===t?[P]:[])];
const enemiesOf=t=>[...bots.filter(b=>b.alive&&b.team!==t),...(P.alive&&P.team!==t?[P]:[])];
const flash=$('flash');
function feed(t){const d=document.createElement('div');d.textContent=t;$('feed').prepend(d);setTimeout(()=>d.remove(),4000)}
function say(t,s){$('msg').textContent=t;clearTimeout(say.k);if(s)say.k=setTimeout(()=>$('msg').textContent='',s*1000)}
function dmgTo(t,d,from){if(!t.alive)return;if(t.arm>0){d*=.55;t.arm=Math.max(0,t.arm-d)}t.hp-=d;bleed(t,from,d);
 if(t===P){sfx.hurt();flash.style.opacity=.9;setTimeout(()=>flash.style.opacity=0,120)}else if(from){t.last=[from.x,from.z];t.lt=6;t.react=.2}
 if(t.hp<=0)kill(t,from)}
function kill(t,from){t.alive=false;t.hp=0;
 if(from&&from.team!==t.team){from.money=Math.min(16000,from.money+800);if(from===P)P.kills++;else chat(from,['изи','ха, лох','держи','слабак','не лезь, дебил']);if(t!==P&&R()<.5)setTimeout(()=>chat(t,['блин, откуда?','чёрт, он тут','вот же гад','лаги какие-то','кто это был?']),500);feed((from===P?'Вы':from.name)+' ► '+(t===P?'Вы':t.name)+' +800$')}
 if(t!==P){let dx=t.x-(from?from.x:t.x-1),dz=t.z-(from?from.z:t.z),m=Math.hypot(dx,dz)||1;dx/=m;dz/=m;
  t.fall=ragStart(t,dx,dz,from?1:0);t.lab.visible=false;splat(new THREE.Vector3(t.x,.02,t.z),new THREE.Vector3(0,1,0),1.6,0)}
 else say('Вас убили',3)}
function fall(b,dt){const f=b.fall;f.w+=dt*28;f.th+=f.w*dt;if(f.th>1.5){f.th=1.5;f.w=f.w>3?-f.w*.25:0}
 b.g.quaternion.setFromAxisAngle(f.ax,f.th).multiply(f.qy);b.g.position.set(b.x+f.vx*f.th,Math.sin(f.th)*.2,b.z+f.vz*f.th);
 b.legs[0].rotation.x=f.l0*f.th;b.legs[1].rotation.x=f.l1*f.th;b.rifle.rotation.x=f.th*.6}

const GR={flash:{n:'Светошумовая',p:200},smoke:{n:'Дымовая',p:300},he:{n:'Граната',p:300},mol:{n:'Молотов',p:400}},GC={flash:0xcccccc,smoke:0x7a8a7a,he:0x3a4a2a,mol:0xc4752a};
const gren=[],fires=[],smokes=[],decals=[];
function wallHit(o,d,max){let best=max,bb=null;for(const b of boxes){const t=rayBox(o,d,b,best);if(t>=0&&t<best){best=t;bb=b}}if(!bb)return null;
 const p=o.clone().addScaledVector(d,best),e=.06,n=new THREE.Vector3();
 if(Math.abs(p.x-bb.x0)<e)n.x=-1;else if(Math.abs(p.x-bb.x1)<e)n.x=1;else if(Math.abs(p.z-bb.z0)<e)n.z=-1;else if(Math.abs(p.z-bb.z1)<e)n.z=1;else return null;return {p,n}}
const bloodT=(()=>{const c=document.createElement('canvas');c.width=c.height=64;const x=c.getContext('2d'),g=x.createRadialGradient(32,32,2,32,32,30);g.addColorStop(0,'rgba(150,10,10,.95)');g.addColorStop(.6,'rgba(120,0,0,.7)');g.addColorStop(1,'rgba(100,0,0,0)');x.fillStyle=g;x.fillRect(0,0,64,64);
 for(let i=0;i<8;i++){x.beginPath();x.arc(32+(R()-.5)*50,32+(R()-.5)*50,2+R()*4,0,7);x.fillStyle='rgba(130,0,0,.8)';x.fill()}return new THREE.CanvasTexture(c)})();
const bloodM=new THREE.MeshBasicMaterial({map:bloodT,transparent:true,depthWrite:false,polygonOffset:true,polygonOffsetFactor:-2});
function splat(p,n,s,drip){const m=new THREE.Mesh(new THREE.PlaneGeometry(s,s),bloodM);m.position.copy(p).addScaledVector(n,.03);
 if(n.y>.5){m.rotation.x=-Math.PI/2;m.rotateZ(R()*6)}else m.lookAt(p.clone().add(n));scene.add(m);decals.push({m,age:0,drip:!!drip,s});if(decals.length>110){scene.remove(decals.shift().m)}}
function bleed(t,from,d){const o=new THREE.Vector3(t.x,1.3,t.z);let dx=from?t.x-from.x:0,dz=from?t.z-from.z:0;const m=Math.hypot(dx,dz)||1;dx/=m;dz/=m;puff(o,6,0x8a0808);
 for(let k=0;k<3;k++){const dv=new THREE.Vector3(dx+(R()-.5)*.8,(R()-.5)*.5,dz+(R()-.5)*.8).normalize();const h=wallHit(o,dv,7);if(h)splat(h.p,h.n,.6+R()*.8,1)}
 if(R()<.5)splat(new THREE.Vector3(t.x+dx*.5,.02,t.z+dz*.5),new THREE.Vector3(0,1,0),.5+R()*.6,0)}
function decUp(dt){for(const d of decals)if(d.drip&&d.age<1.6){d.age+=dt;const ds=dt*1.4;d.m.scale.y+=ds;d.m.position.y-=.5*d.s*ds}}
function clearFx(){[decals,gren,smokes,fires].forEach(a=>{a.forEach(x=>scene.remove(x.m));a.length=0})}
const cloudT=(()=>{const c=document.createElement('canvas');c.width=c.height=128;const x=c.getContext('2d');for(let k=0;k<14;k++){const px=64+(R()-.5)*50,py=64+(R()-.5)*50,g=x.createRadialGradient(px,py,0,px,py,30+R()*20);g.addColorStop(0,'rgba(255,255,255,.35)');g.addColorStop(1,'rgba(255,255,255,0)');x.fillStyle=g;x.fillRect(0,0,128,128)}return new THREE.CanvasTexture(c)})();
function smokeHole(o,d,len){for(const s of smokes)for(const c of s.m.children){const u=c.userData,px=s.x+c.position.x-o.x,py=c.position.y-o.y,pz=s.z+c.position.z-o.z,tc=px*d.x+py*d.y+pz*d.z;if(tc<0||tc>len)continue;
 if(px*px+py*py+pz*pz-tc*tc<1.4){u.hole=3+R()*2;u.px+=(R()-.5)*1.2;u.pz+=(R()-.5)*1.2}}}
function smoked(ax,az,bx_,bz){if(!smokes.length)return false;const dx=bx_-ax,dz=bz-az,L=Math.hypot(dx,dz),n=Math.ceil(L/1.2);
 for(let k=1;k<n;k++){const x=ax+dx*k/n,z=az+dz*k/n;for(const s of smokes)for(const c of s.m.children)if(c.userData.op>.22&&Math.abs(c.position.y-1.5)<2.2&&Math.hypot(s.x+c.position.x-x,s.z+c.position.z-z)<1.5)return true}return false}
function throwG(o,type,pos,dir,spd){const m=new THREE.Mesh(new THREE.CylinderGeometry(.05,.05,.14,8),new THREE.MeshStandardMaterial({color:GC[type]}));m.position.copy(pos);scene.add(m);
 gren.push({m,type,o,v:dir.clone().multiplyScalar(spd).add(new THREE.Vector3(0,3.5,0)),t:type==='mol'?9:type==='smoke'?1.3:type==='flash'?1.4:1.8})}
function boom(g){const p=g.m.position,o=g.o;
 if(g.type==='he'){puff(p,25,0xffa030);puff(p,10,0x444444);sfx.boom();for(const a of enemiesOf(o.team)){const dx=a.x-p.x,dz=a.z-p.z,d=Math.hypot(dx,dz);if(d<9){_e.set(p.x,Math.max(.8,p.y),p.z);_f.set(dx,0,dz).normalize();if(d<1||wallDist(_e,_f,d)>=d-.1)dmgTo(a,120*(1-d/9),o)}}}
 else if(g.type==='flash'){sfx.noise(.5,6000,1.2,'highpass');sfx.tone(3000,.5,.3,'sine',500);puff(p,12,0xffffff);
  for(const a of [...enemiesOf(o.team),...mates(o.team).filter(q=>q.alive)]){const dx=a.x-p.x,dz=a.z-p.z,d=Math.hypot(dx,dz);if(d<30){_e.set(p.x,Math.max(1,p.y),p.z);_f.set(dx,0,dz).normalize();
   if(d<1||wallDist(_e,_f,d)>=d-.1){let t=4*(1-d/30);if(a===P){cam.getWorldDirection(fw);t*=((-dx*fw.x-dz*fw.z)/(d||1))>0?1:.35;P.blind=Math.max(P.blind||0,t)}else a.blind=Math.max(a.blind||0,t)}}}}
 else if(g.type==='smoke'){sfx.noise(1.2,2500,.5,'bandpass');const gr=new THREE.Group();for(let k=0;k<40;k++){const sp=new THREE.Sprite(new THREE.SpriteMaterial({map:cloudT,color:0xd2d4d6,transparent:true,opacity:0,depthWrite:false,fog:true}));const a=R()*6.28,r=Math.sqrt(R())*3.2;
 sp.userData={bx:Math.cos(a)*r,by:.4+R()*3.2,bz:Math.sin(a)*r,op:0,hole:0,px:0,pz:0};sp.scale.set(3.4+R()*2,3.4+R()*2,1);gr.add(sp)}gr.position.set(p.x,0,p.z);scene.add(gr);smokes.push({x:p.x,z:p.z,t:18,age:0,m:gr})}
 else{sfx.noise(.6,1200,.8);const d=new THREE.Mesh(new THREE.CircleGeometry(3.2,24),new THREE.MeshBasicMaterial({color:0xff5a00,transparent:true,opacity:.55,depthWrite:false}));d.rotation.x=-Math.PI/2;d.position.set(p.x,.05,p.z);scene.add(d);fires.push({x:p.x,z:p.z,t:7,m:d,o})}}
function grenUp(dt){for(let i=gren.length-1;i>=0;i--){const g=gren[i],p=g.m.position;g.t-=dt;g.v.y-=13*dt;p.addScaledVector(g.v,dt);
  if(p.y<.1){p.y=.1;g.v.y*=-.35;g.v.x*=.6;g.v.z*=.6;if(g.type==='mol')g.t=0}if(hits(p.x,p.z,.12)){p.x-=g.v.x*dt;p.z-=g.v.z*dt;g.v.x*=-.4;g.v.z*=-.4}g.m.rotation.x+=dt*8;
  if(g.t<=0){boom(g);scene.remove(g.m);gren.splice(i,1)}}
 for(let i=smokes.length-1;i>=0;i--){const s=smokes[i];s.t-=dt;s.age+=dt;const gw=Math.min(1,s.age/1.4),fd=Math.min(1,s.t/3);
  s.m.children.forEach(c=>{const u=c.userData;if(u.hole>0)u.hole-=dt;const tg=(u.hole>0?0:.55)*fd;u.op+=(tg-u.op)*Math.min(1,dt*(u.hole>0?10:1.5));c.material.opacity=u.op;u.px*=1-dt*.4;u.pz*=1-dt*.4;c.position.set(u.bx*gw+u.px,u.by*gw+.2,u.bz*gw+u.pz)});
  if(s.t<=0){scene.remove(s.m);smokes.splice(i,1)}}
 for(let i=fires.length-1;i>=0;i--){const f=fires[i];f.t-=dt;f.m.material.opacity=.4+Math.sin(f.t*20)*.15;
  const m=new THREE.Mesh(new THREE.BoxGeometry(.12,.12,.12),new THREE.MeshBasicMaterial({color:R()<.5?0xff7a00:0xffcc33,transparent:true}));m.position.set(f.x+(R()-.5)*5,.1,f.z+(R()-.5)*5);scene.add(m);fx.push({m,v:new THREE.Vector3(0,3+R()*2,0),l:.5});
  for(const a of mates(0).concat(mates(1)))if(a.alive&&Math.hypot(a.x-f.x,a.z-f.z)<3.2){a.hp-=14*dt;if(a.hp<=0)kill(a,f.o)}
  if(f.t<=0){scene.remove(f.m);fires.splice(i,1)}}}
function throwP(){const k=P.gsel;if(!P.alive||G.ph!=='live'||!k||!P.gr[k])return;P.gr[k]=0;cam.getWorldDirection(fw);throwG(P,k,cam.position.clone().addScaledVector(fw,.6),fw,16);P.gsel=Object.keys(P.gr).find(x=>P.gr[x])||null}
function cycleG(){const ks=Object.keys(P.gr).filter(x=>P.gr[x]);if(ks.length)P.gsel=ks[(ks.indexOf(P.gsel)+1)%ks.length]}
// ragdoll: limbs are separate bodies tied to the torso by springs
const _q=new THREE.Quaternion(),_ax=new THREE.Vector3(),_M=new THREE.Matrix4(),_a=new THREE.Vector3(),_u=new THREE.Vector3();
function ragStart(b,dx,dz,hit){b.g.updateMatrixWorld(true);const parts=[b.tor,b.hd,b.legs[0],b.legs[1],b.rifle];b.rest=parts.map(p=>({p:p.position.clone(),q:p.quaternion.clone()}));
 const sp=hit?5:2,tv=new THREE.Vector3(dx*sp,2+R()*1.5,dz*sp),anc=[null,[0,.55,0],[-.13,-.3,0],[.13,-.3,0],[.1,.05,.25]];
 b.rag=parts.map((p,i)=>{scene.attach(p);return {m:p,v:tv.clone().add(new THREE.Vector3((R()-.5)*(i?5:1),(R()-.5)*(i?3:0),(R()-.5)*(i?5:1))),w:new THREE.Vector3(dz*(i?3:5)+(R()-.5)*3,(R()-.5)*3,-dx*(i?3:5)+(R()-.5)*3),anc:anc[i]&&new THREE.Vector3(...anc[i])}});b.ragT=0;return 1}
function ragEnd(b){if(!b.rag)return;b.rag.forEach((r,i)=>{b.g.add(r.m);r.m.position.copy(b.rest[i].p);r.m.quaternion.copy(b.rest[i].q)});b.rag=null}
function ragUp(dt){dt=Math.min(dt,.02);for(const b of bots.concat([...rem.values()])){if(!b.rag||b.ragT>6)continue;b.ragT+=dt;const T=b.rag[0];
 b.rag.forEach((r,i)=>{const m=r.m;
  if(i){_a.copy(r.anc).applyQuaternion(T.m.quaternion).add(T.m.position);r.v.x+=((_a.x-m.position.x)*300-(r.v.x-T.v.x)*14)*dt;r.v.y+=((_a.y-m.position.y)*300-(r.v.y-T.v.y)*14)*dt;r.v.z+=((_a.z-m.position.z)*300-(r.v.z-T.v.z)*14)*dt}
  r.v.y-=14*dt;m.position.addScaledVector(r.v,dt);let fl=i?.12:.22;
  if(!i){_M.makeRotationFromQuaternion(m.quaternion);const e=_M.elements;fl=.5*(.56*Math.abs(e[1])+.6*Math.abs(e[5])+.32*Math.abs(e[9]));_u.set(e[4],e[5],e[6]);
   if(Math.abs(_u.y)>.25&&m.position.y<fl+.3){_ax.set(0,1,0).cross(_u).multiplyScalar(Math.sign(_u.y));r.w.addScaledVector(_ax,dt*25)}}
  if(m.position.y<fl){m.position.y=fl;r.v.y*=-.25;r.v.x*=.8;r.v.z*=.8;r.w.multiplyScalar(.85)}
  if(m.position.y<fl+.05){const k=1-Math.min(1,dt*6);r.v.x*=k;r.v.z*=k}
  if(hits(m.position.x,m.position.z,.25)){m.position.x-=r.v.x*dt;m.position.z-=r.v.z*dt;r.v.x*=-.3;r.v.z*=-.3}
  r.w.multiplyScalar(1-Math.min(1,dt*(m.position.y<fl+.1?4:.8)));if(i)m.quaternion.slerp(T.m.quaternion,dt*1.5);
  const wl=r.w.length();if(wl>1e-4){_q.setFromAxisAngle(_ax.copy(r.w).divideScalar(wl),wl*dt);m.quaternion.premultiply(_q)}})}}
// online (room): other viewers appear as enemy players
let ROOM=null,myPeer=null,nt=0;const rem=new Map(),myNick='Игрок'+(100+Math.floor(R()*900));
async function netInit(){try{if(typeof claude==='undefined')return;const r=await claude.use('room');if(!r)return;ROOM=r;
 r.onPeers(c=>{for(const p of c.peers){if(p.isMe){if(p.sameTab)myPeer=p.peer;continue}if(p.kind!=='viewer')continue;let a=rem.get(p.peer);const d=p.presence||{};
  if(!a){a={name:d.nm||'Игрок',team:1-P.team,x:d.x||0,z:d.z||0,tx:d.x||0,tz:d.z||0,yaw:0,hp:100,alive:true,peer:p.peer,ph:0,t:0,g:null};skin(a);rem.set(p.peer,a)}
  if(a.team!==1-P.team){a.team=1-P.team;skin(a)}
  if(d.x!==undefined){a.tx=d.x;a.tz=d.z;a.yaw=d.yaw||0;const al=!!d.al;if(a.alive&&!al){a.alive=false;a.lab.visible=false;a.fall=ragStart(a,0,0,1)}else if(!a.alive&&al){ragEnd(a);a.alive=true;a.lab.visible=true}}}
  for(const p of c.left){const a=rem.get(p.peer);if(a){ragEnd(a);scene.remove(a.g);rem.delete(p.peer)}}});
 r.on('hit',m=>{const d=m.data;if(d&&d.to===myPeer&&P.alive&&G.ph==='live')dmgTo(P,Math.min(120,+d.d||0),{x:P.x+1,z:P.z,team:1-P.team,name:d.nm,money:0})});
 r.on('shot',m=>{if(m.isMe)return;const d=m.data;if(!d)return;tracer(new THREE.Vector3(d.x,1.3,d.z),new THREE.Vector3(d.tx,d.ty,d.tz));sfx.shot(Math.max(.05,.6-Math.hypot(P.x-d.x,P.z-d.z)/70))})}catch(e){}}
function netTick(dt){if(!ROOM)return;nt+=dt;if(nt>.1){nt=0;ROOM.presence({x:+P.x.toFixed(2),z:+P.z.toFixed(2),yaw:+P.yaw.toFixed(2),al:P.alive?1:0,nm:myNick})}
 for(const a of rem.values()){if(!a.alive)continue;const k=Math.min(1,dt*10),ox=a.x,oz=a.z;a.x+=(a.tx-a.x)*k;a.z+=(a.tz-a.z)*k;const sp=Math.hypot(a.x-ox,a.z-oz)/Math.max(dt,.001);a.ph+=dt*sp*2.2;const sw=Math.sin(a.ph),am=Math.min(1,sp/3);
  a.legs.forEach((l,i)=>{const q=i?-sw:sw;l.rotation.x=q*.8*am;l.userData.k.rotation.x=Math.max(0,-q)*1.1*am});a.g.position.set(a.x,Math.abs(sw)*.05*am,a.z);a.g.rotation.y=a.yaw+Math.PI;a.rifle.rotation.x=-.05}}
// chat
let chatT=0;
function chat(a,pool,force){if(!running)return;const now=performance.now();if(!force&&now-chatT<700)return;chatT=now;const d=document.createElement('div'),mate=a.team===P.team;
 d.innerHTML='<span style="color:'+(mate?'#6fe3ff':'#ff6a4a')+'">'+(mate?'[Команда] ':'[Все] ')+a.name+'</span>: '+pool[Math.floor(R()*pool.length)];$('chat').appendChild(d);while($('chat').children.length>7)$('chat').firstChild.remove();setTimeout(()=>d.remove(),9000)}
// bots AI
const WP=[[0,50],[0,30],[0,5],[0,-10],[20,-14],[-20,-14],[41,30],[-45,32],[41,-10],[-46,5],[20,30],[-20,30]];
const _o=new THREE.Vector3(),_d=new THREE.Vector3();
function clear(x,z,a,len){_o.set(x,.6,z);_d.set(Math.sin(a),0,Math.cos(a));return wallDist(_o,_d,len)>=len-.01}
function steer(b,tx,tz,sp,dt){const base=Math.atan2(tx-b.x,tz-b.z);for(const o of [0,.5,-.5,1,-1,1.6,-1.6,2.4]){const a=base+o*b.sd;if(clear(b.x,b.z,a,2.2)){move(b,Math.sin(a)*sp*dt,Math.cos(a)*sp*dt,.45);return a}}b.sd=-b.sd;return base}
function plant(x,z,who){const B=G.bomb;if(B.on)return;B.on=1;B.x=x;B.z=z;B.t=40;B.bt=0;bombM.position.set(x,0,z);bombM.visible=true;who.money=Math.min(16000,who.money+300);say('Бомба заложена!',2.5);sfx.beep();G.nz.push([x,z,0]);const si=Math.hypot(x-SITE[0][0],z-SITE[0][1])<Math.hypot(x-SITE[1][0],z-SITE[1][1])?'A':'B';if(who!==P)chat(who,['плент! прикрывайте','бомба заложена, держим']);const cb=bots.filter(q=>q.alive&&q.team===1)[0];if(cb)setTimeout(()=>chat(cb,['бомба на '+si+', бегом!','блин, заложили '+si]),900)}
function defuse(who){if(who!==P)chat(who,['дефуз!','успел, гг']);G.bomb.on=0;who.money=Math.min(16000,who.money+2000);bombM.visible=false;endRound(1,'Бомба обезврежена')}
const _e=new THREE.Vector3(),_f=new THREE.Vector3();
function botAI(b,dt){const w=W[b.w];b.t+=dt;b.cd-=dt;b.react-=dt;b.blind=Math.max(0,(b.blind||0)-dt);b.gcd=(b.gcd||0)-dt;b.rl=Math.max(0,b.rl-dt);const B=G.bomb;
 let tg=null,td=60;for(const e of enemiesOf(b.team)){const dx=e.x-b.x,dz=e.z-b.z,d=Math.hypot(dx,dz);if(d<td&&!(b.blind>0)&&!smoked(b.x,b.z,e.x,e.z)){_e.set(b.x,1.5,b.z);_f.set(dx,0,dz).normalize();if(wallDist(_e,_f,d)>=d-.05){tg=e;td=d}}}
 let speed=0,face=0,aim=0;
 if(tg){const dx=tg.x-b.x,dz=tg.z-b.z;face=Math.atan2(dx,dz);if(!b.seen){b.seen=1;b.react=.3+R()*.25;if(R()<.25)chat(b,['вижу '+tg.name,'контакт!','они тут!'])}b.last=[tg.x,tg.z];b.lt=6;b.act=0}else{b.seen=0;b.lt-=dt;
  for(const n of G.NZ)if(n[2]!==b.team&&b.lt<=0&&Math.hypot(n[0]-b.x,n[1]-b.z)<45&&R()<.1){b.last=[n[0]+(R()-.5)*6,n[1]+(R()-.5)*6];b.lt=6}}
 if(tg&&b.gr&&b.gr.length&&b.gcd<=0&&td>9&&td<40&&b.rl<=0){const ty=b.gr.pop();b.gcd=3;const dr=new THREE.Vector3(tg.x-b.x,0,tg.z-b.z).normalize();dr.y=.25;dr.normalize();throwG(b,ty,new THREE.Vector3(b.x,1.6,b.z),dr,Math.min(18,6+td*.55));chat(b,['граната!','кидаю флешку','держите дым','гори!'])}
 if(b.rl>0){if(tg&&td<30){steer(b,b.x-(tg.x-b.x),b.z-(tg.z-b.z),2.8,dt);speed=2.8}}
 else if(b.hp<35&&tg){steer(b,b.x-(tg.x-b.x),b.z-(tg.z-b.z),4,dt);speed=4}
 else if(tg){aim=1;const dx=tg.x-b.x,dz=tg.z-b.z;
  b.sp-=dt;if(b.sp<=0){b.sp=.5+R()*.9;b.st=R()<.45?0:(R()<.5?1:-1)}
  if(b.st){const a=face+Math.PI/2*b.st;if(clear(b.x,b.z,a,1.5)){move(b,Math.sin(a)*3*dt,Math.cos(a)*3*dt,.45);speed=3}else b.st=-b.st}
  else if(td>22){steer(b,tg.x,tg.z,3.2,dt);speed=3.2}
  if(b.react<=0&&b.cd<=0){if(b.burst<=0)b.burst=w.r>.5?1:3+Math.floor(R()*3);b.burst--;b.cd=b.burst<=0?w.r+.4+R()*.7:w.r*(1+R()*.3);b.ammo--;b.kick=1;
   let hit=Math.max(.05,.6-td/90-(speed?.25:0)-w.s*3);if(w.pel>1&&td>15)hit*=.3;
   G.nz.push([b.x,b.z,b.team]);const dp=Math.hypot(P.x-b.x,P.z-b.z);sfx.shot(Math.max(.05,.6-dp/70),w.r>.5?.7:1);
   _e.set(b.x,1.3,b.z);const tb=new THREE.Vector3(tg.x,1.1+R()*.7,tg.z);
   if(R()<hit)dmgTo(tg,w.pel>1?w.d*3:w.d,b);else{tb.x+=(R()-.5)*3;tb.y+=R()-.5}tracer(_e,tb);smokeHole(_e,tb.clone().sub(_e).normalize(),_e.distanceTo(tb));
   if(b.ammo<=0){b.ammo=w.m;b.rl=w.rl;if(dp<30)sfx.click()}}}
 else{let goal=null;
  if(b.team===0){if(!B.on){goal=SITE[b.site];if(Math.hypot(goal[0]-b.x,goal[1]-b.z)<5){b.act+=dt;speed=-1;if(b.act>=3){plant(b.x,b.z,b);b.act=0}}else b.act=0}else goal=[B.x+b.gx,B.z+b.gz]}
  else{if(B.on){goal=[B.x,B.z];if(Math.hypot(B.x-b.x,B.z-b.z)<2.5){b.act+=dt;speed=-1;if(b.act>=(b.kit?2.5:5))defuse(b)}}else goal=HOLD[b.site%3]}
  if(b.lt>0&&b.last&&speed>=0&&!(b.team&&B.on))goal=b.last;
  if(speed>=0&&goal){if(Math.hypot(goal[0]-b.x,goal[1]-b.z)>1.8){face=steer(b,goal[0],goal[1],b.team===0&&!B.on?4:3.6,dt);speed=4}else if(b.last&&goal===b.last)b.lt=0;face=face||Math.atan2(goal[0]-b.x,goal[1]-b.z)}
  if(speed<0){speed=0;face=Math.atan2(B.on?B.x-b.x:SITE[b.site][0]-b.x,B.on?B.z-b.z:SITE[b.site][1]-b.z)}}
 for(const o of bots)if(o!==b&&o.alive){const sx=b.x-o.x,sz=b.z-o.z,sd=Math.hypot(sx,sz);if(sd<1.6&&sd>0)move(b,sx/sd*dt*2,sz/sd*dt*2,.45)}
 b.ph+=dt*speed*2.2;const sw=Math.sin(b.ph),amt=Math.min(1,speed/3),cr=b.rl>0?.5:0;
 b.legs.forEach((l,i)=>{const s=i?-sw:sw;l.rotation.x=s*.8*amt-cr;l.userData.k.rotation.x=Math.max(0,-s)*1.1*amt+cr*1.4});
 b.g.position.set(b.x,-cr*.35+Math.abs(sw)*.05*amt,b.z);
 let df=face-b.g.rotation.y;while(df>Math.PI)df-=2*Math.PI;while(df<-Math.PI)df+=2*Math.PI;b.g.rotation.y+=df*Math.min(1,dt*10);b.g.rotation.z=sw*.04*amt;
 b.kick=Math.max(0,b.kick-dt*10);b.rifle.rotation.x=b.rl>0?.7+Math.sin(b.t*6)*.05:(aim?-.05:.25);b.rifle.position.set(.05,b.rl>0?1.05:1.25,.2-b.kick*.08);b.mag.visible=!(b.rl>.8&&b.rl<1.5)}

// economy / buying
function botBuy(b){const m=b.money,rifle=b.team?3:4,buy=(i)=>{b.money-=i;};
 const arm=()=>{if(b.money>=650&&!b.arm){b.money-=650;b.arm=100}},kit=()=>{if(b.team&&b.money>=400&&!b.kit){b.money-=400;b.kit=1}};
 if(b.w===0){if(m>=3350){let i=rifle;const r=R();if(m>=5850&&r<.1)i=6;else if(m>=5400&&r<.25)i=5;b.w=i;b.money-=W[i].p;arm();kit()}
  else if(m>=2700&&R()<.4){b.w=rifle;b.money-=2700;kit()}
  else if(m>=1200&&R()<.5){const i=(m>=1800&&R()<.4)?2:1;b.w=i;b.money-=W[i].p;arm()}
  else if(R()<.5)arm()}else{arm();kit()}
 b.ammo=W[b.w].m;b.gr=[];const ks=Object.keys(GR);for(let k=0;k<2;k++){const t=ks[Math.floor(R()*4)];if(b.money>=GR[t].p&&R()<.5){b.money-=GR[t].p;b.gr.push(t)}}if(R()<.3)chat(b,b.w?['фулл бай','берём стволы']:['эко, сэйвимся','пистолеты, народ'])}
function startRound(){G.round++;G.ph='buy';clearFx();G.t=10;G.bomb={on:0};bombM.visible=false;
 [0,1].forEach(t=>{const sp=SPAWNS[t].slice().sort(()=>R()-.5);mates(t).forEach((a,i)=>{const s=sp[i];a.dead=!a.alive;a.x=s[0];a.z=s[1];a.hp=100;a.alive=true;a.act=0;
  if(a!==P){a.g.quaternion.identity();a.g.rotation.set(0,t?0:Math.PI,0);a.fall=null;ragEnd(a);a.lab.visible=true;a.last=null;a.lt=0;a.rl=0;a.seen=0;a.site=t?Math.floor(R()*3):(i%2);a.gx=(R()-.5)*14;a.gz=(R()-.5)*8;
   if(a.dead){a.w=0;a.arm=0;a.kit=0}a.dead=0;botBuy(a)}})});
 if(P.dead){P.pri=0;P.arm=0;P.kit=0;P.gr={flash:0,smoke:0,he:0,mol:0};P.gsel=null}P.dead=0;P.cur=P.pri;P.hp=100;P.alive=true;P.reload=0;P.act=0;P.yaw=P.team?Math.PI:0;P.pitch=0;P.x=SPAWNS[P.team][0][0]+((Math.random()-.5)*6);P.z=SPAWNS[P.team][0][1];
 for(const i in P.ammo)P.ammo[i]=W[i].m;mkGun(W[P.cur]);say('Раунд '+G.round+': закупка',3);G.over=0}
const SPAWNS=[[[0,54],[-9,53],[-4.5,56],[4.5,56],[9,53]],[[0,-54],[-9,-54],[-4.5,-56],[4.5,-56],[9,-54]]];
function endRound(winTeam,txt){if(G.ph==='end')return;G.ph='end';G.t=5;const sq=winTeam===P.team?0:1;G.sc[sq]++;G.loss[winTeam]=0;G.loss[1-winTeam]=Math.min(4,G.loss[1-winTeam]+1);
 mates(0).concat(mates(1)).forEach(a=>{a.money=Math.min(16000,a.money+(a.team===winTeam?3250:1400+500*G.loss[a.team]))});
 say((sq?'Раунд проигран. ':'Раунд выигран! ')+(txt||''),4);const wb=bots.filter(q=>q.team===winTeam)[0],lb=bots.filter(q=>q.team!==winTeam)[0];if(wb)chat(wb,['гг','изи катка','вот это раунд'],1);if(lb)setTimeout(()=>chat(lb,['чёрт','какие же вы тупые','не повезло, блин']),800)}
function afterRound(){if(G.round>=10){G.over=1;const s=G.sc;$('start').style.display='flex';$('start').innerHTML='<h1>'+(s[0]>s[1]?'Победа':s[0]<s[1]?'Поражение':'Ничья')+'</h1><p>Счёт '+s[0]+' : '+s[1]+'. Убийств: '+P.kills+'.</p><button id="go2">Играть снова</button>';$('go2').onclick=()=>location.reload();return}
 if(G.round===5){bots.forEach(b=>{b.team^=1;b.money=800;b.w=0;b.arm=0;b.kit=0;b.dead=0;skin(b)});P.team^=1;P.money=800;P.pri=0;P.arm=0;P.kit=0;P.dead=0;G.loss=[0,0];say('Смена сторон!',2.5)}
 startRound()}

// shop
function shopOpen(){const g=$('grid');g.innerHTML='';$('sh').textContent='Магазин   '+P.money+' $';
 const add=(t,pr,own,fn)=>{const d=document.createElement('div');d.className='it';d.innerHTML='<b>'+t+'</b><br>'+(own||pr+' $');if(own)d.style.opacity=.4;
  d.onclick=()=>{if(own||P.money<pr||!P.alive)return;P.money-=pr;fn();sfx.buy();shopOpen()};g.appendChild(d)};
 W.forEach((w,i)=>{if(i)add(w.n+'<br>урон '+w.d+(w.pel>1?'x'+w.pel:'')+', маг. '+w.m,w.p,P.pri===i?'Куплено':P.pri?'Слот занят':'',()=>{P.pri=i;P.cur=i;P.ammo[i]=w.m;mkGun(w)})});
 add('Бронежилет',650,P.arm>0?'Куплено':'',()=>P.arm=100);if(P.team)add('Набор сапёра',400,P.kit?'Куплено':'',()=>P.kit=1);
 for(const k in GR)add(GR[k].n,GR[k].p,P.gr[k]>0?'Куплено':'',()=>{P.gr[k]=1;if(!P.gsel)P.gsel=k});$('shop').style.display='block'}
$('shopBtn').onclick=shopOpen;$('close').onclick=()=>$('shop').style.display='none';

// player
const fw=new THREE.Vector3(),org=new THREE.Vector3(),dd=new THREE.Vector3();
function reload(){const w=W[P.cur];if(P.reload<=0&&P.ammo[P.cur]<w.m&&P.alive){P.reload=w.rl;sfx.click();setTimeout(()=>sfx.click(),w.rl*400)}}
function shoot(){const w=W[P.cur];if(!P.alive||G.ph!=='live'||P.reload>0||P.cool>0)return;if(P.ammo[P.cur]<=0){reload();return}
 P.ammo[P.cur]--;P.cool=w.r;P.pitch+=.008+w.d*.0001;cam.getWorldDirection(fw);org.copy(cam.position);G.nz.push([P.x,P.z,P.team]);
 let tot=new Map(),last=null;
 for(let k=0;k<w.pel;k++){dd.copy(fw);dd.x+=(R()-.5)*w.s*2;dd.y+=(R()-.5)*w.s*2;dd.z+=(R()-.5)*w.s*2;dd.normalize();
  let bt=wallDist(org,dd,100),best=null,head=false;smokeHole(org,dd,bt);
  for(const b of bots.concat([...rem.values()])){if(!b.alive)continue;for(const [y,r,h] of [[1.75,.25,1],[1.2,.45,0],[.6,.4,0]]){const vx=b.x-org.x,vy=y-org.y,vz=b.z-org.z,tc=vx*dd.x+vy*dd.y+vz*dd.z;if(tc<0||tc>bt)continue;if(vx*vx+vy*vy+vz*vz-tc*tc<r*r){best=b;bt=tc;head=!!h}}}
  const ip=org.clone().addScaledVector(dd,bt);last=ip;
  if(best&&best.team!==P.team){tot.set(best,(tot.get(best)||0)+w.d*(head?2.5:1));puff(ip,5,0xaa1111)}else if(!best)puff(ip,w.pel>1?2:8,0xd9c49a);}
 const mp=gunH.localToWorld(new THREE.Vector3(0,.015,-.6));tracer(mp,last);
 tot.forEach((d,b)=>{if(b.peer){if(ROOM)ROOM.emit('hit',{to:b.peer,d:Math.round(d),nm:myNick})}else dmgTo(b,d,P);sfx.hit()});if(ROOM&&last)ROOM.emit('shot',{x:+P.x.toFixed(1),z:+P.z.toFixed(1),tx:+last.x.toFixed(1),ty:+last.y.toFixed(1),tz:+last.z.toFixed(1)});
 gunH.position.z=-.48;setTimeout(()=>gunH.position.z=-.55,60);mf.visible=true;mf.rotation.z=R()*3;setTimeout(()=>mf.visible=false,45);sfx.shot(1,w.r>.5?.7:1);
 if(P.ammo[P.cur]<=0)reload()}
function swap(){if(!P.alive){P.sp=(P.sp||0)+1;return}if(P.pri){P.cur=P.cur?0:P.pri;P.reload=0;mkGun(W[P.cur])}}

// input
const keys={};let mvx=0,mvz=0,firing=false,holdAct=false;
addEventListener('keydown',e=>{keys[e.code]=1;if(e.code==='KeyR')reload();if(e.code==='KeyE')holdAct=true;if(e.code==='KeyB')shopOpen()});addEventListener('keyup',e=>{keys[e.code]=0;if(e.code==='KeyE')holdAct=false});
const stick=$('stick'),knob=$('knob');let sid=null;
function sm(e){const r=stick.getBoundingClientRect();let x=e.clientX-(r.left+r.width/2),y=e.clientY-(r.top+r.height/2);const m=Math.hypot(x,y),k=Math.min(m,55)/(m||1);x*=k;y*=k;knob.style.transform=`translate(${x}px,${y}px)`;mvx=x/55;mvz=y/55}
stick.addEventListener('pointerdown',e=>{sid=e.pointerId;stick.setPointerCapture(sid);sm(e)});stick.addEventListener('pointermove',e=>{if(e.pointerId===sid)sm(e)});
const se=e=>{if(e.pointerId===sid){sid=null;mvx=mvz=0;knob.style.transform=''}};stick.addEventListener('pointerup',se);stick.addEventListener('pointercancel',se);
const look=$('look');let lid=null,lx=0,ly=0;
look.addEventListener('pointerdown',e=>{if(lid===null){lid=e.pointerId;look.setPointerCapture(lid);lx=e.clientX;ly=e.clientY}});
look.addEventListener('pointermove',e=>{if(e.pointerId!==lid)return;P.yaw-=(e.clientX-lx)*.006;P.pitch=Math.max(-1.3,Math.min(1.3,P.pitch-(e.clientY-ly)*.006));lx=e.clientX;ly=e.clientY});
const le=e=>{if(e.pointerId===lid)lid=null};look.addEventListener('pointerup',le);look.addEventListener('pointercancel',le);
function hold(el,on,off){let id=null;el.addEventListener('pointerdown',e=>{id=e.pointerId;el.setPointerCapture(id);on()});const f=e=>{if(e.pointerId===id){id=null;off()}};el.addEventListener('pointerup',f);el.addEventListener('pointercancel',f)}
hold($('fire'),()=>firing=true,()=>firing=false);hold($('act'),()=>holdAct=true,()=>holdAct=false);$('rel').addEventListener('pointerdown',reload);$('sw').addEventListener('pointerdown',swap);$('gr').addEventListener('pointerdown',throwP);$('grs').addEventListener('pointerdown',cycleG);

let running=false,last=performance.now();
$('go').onclick=()=>{sfx.init();$('start').style.display='none';running=true;last=performance.now();startRound()};
function hud(){const w=W[P.cur],B=G.bomb;$('hp').textContent='HP '+Math.max(0,Math.ceil(P.hp))+(P.arm>0?'  Б '+Math.ceil(P.arm):'');$('mon').textContent=P.money+' $';
 $('ammo').textContent=P.reload>0?'Перезарядка':w.n+' '+P.ammo[P.cur]+'/'+w.m;
 const t=Math.max(0,Math.ceil(B.on?B.t:G.t));$('top').textContent='Раунд '+G.round+'/10   Вы '+G.sc[0]+' : '+G.sc[1]+' Враги   '+(B.on?'БОМБА ':G.ph==='buy'?'Закупка ':'')+Math.floor(t/60)+':'+String(t%60).padStart(2,'0')+'   '+(P.team?'Защита':'Атака')+(ROOM?'   Онлайн '+(rem.size+1):'');
 $('shopBtn').style.display=G.ph==='buy'&&P.alive?'flex':'none';
 const ab=$('act');let txt='';if(P.alive&&G.ph==='live'){if(P.team===0&&!B.on&&SITE.some(s=>Math.hypot(s[0]-P.x,s[1]-P.z)<6))txt='Заложить';if(P.team===1&&B.on&&Math.hypot(B.x-P.x,B.z-P.z)<3)txt='Обезвредить'}
 ab.style.display=txt?'flex':'none';ab.textContent=txt;P.can=txt;const hg=P.gsel&&P.alive?'flex':'none';$('gr').style.display=hg;$('grs').style.display=hg;$('grs').textContent=P.gsel?GR[P.gsel].n.split(' ')[0]:''}
function loop(now){requestAnimationFrame(loop);const dt=Math.min(.05,(now-last)/1000);last=now;
 if(running&&!G.over){const B=G.bomb;G.t-=dt;G.NZ=G.nz;G.nz=[];
  if(G.ph==='buy'&&G.t<=0){G.ph='live';G.t=100;$('shop').style.display='none';say('Раунд начался!',2)}
  else if(G.ph==='end'&&G.t<=0)afterRound();
  if(G.ph==='live'){
   if(B.on){B.t-=dt;B.bt-=dt;if(B.bt<=0){B.bt=Math.max(.15,B.t/40);sfx.beep()}if(B.t<=0){sfx.boom();puff(new THREE.Vector3(B.x,1,B.z),40,0xffa030);bombM.visible=false;B.on=0;
     mates(0).concat(mates(1)).forEach(a=>{if(a.alive&&Math.hypot(a.x-B.x,a.z-B.z)<14)kill(a,null)});endRound(0,'Бомба взорвалась')}}
   else if(G.t<=0)endRound(1,'Время вышло');
   const aT=mates(0).filter(a=>a.alive).length,aC=mates(1).filter(a=>a.alive).length;
   if(!B.on&&aC===0)endRound(0,'Защитники уничтожены');else if(!B.on&&aT===0)endRound(1,'Атакующие уничтожены');else if(B.on&&aC===0)endRound(0,'Защитники уничтожены')}
  if(P.alive&&G.ph!=='end'||P.alive){let ix=mvx+(keys.KeyD?1:0)-(keys.KeyA?1:0),iz=mvz+(keys.KeyS?1:0)-(keys.KeyW?1:0);if(G.ph==='buy'){ix=iz=0}
   const m=Math.hypot(ix,iz);if(m>1){ix/=m;iz/=m}const c=Math.cos(P.yaw),s=Math.sin(P.yaw);P.mv=Math.min(1,m);P.bt=(P.bt||0)+dt*P.mv*9;move(P,(ix*c+iz*s)*6*dt,(-ix*s+iz*c)*6*dt,.4);
   if(firing||keys.KeyF)shoot();
   if(holdAct&&P.can&&P.mv<.3){P.act+=dt;say((P.can==='Заложить'?'Закладка ':'Обезвреживание ')+Math.min(100,Math.floor(P.act/(P.can==='Заложить'?3:(P.kit?2.5:5))*100))+'%');
    if(P.can==='Заложить'&&P.act>=3){plant(P.x,P.z,P);P.act=0}else if(P.can==='Обезвредить'&&P.act>=(P.kit?2.5:5)){defuse(P);P.act=0}}else if(P.act>0){P.act=0;say('')}}
  P.cool-=dt;if(P.reload>0){P.reload-=dt;if(P.reload<=0)P.ammo[P.cur]=W[P.cur].m}
  for(const b of bots){if(b.alive){if(G.ph==='live')botAI(b,dt);else{b.g.position.set(b.x,0,b.z)}}}
  dust.position.set(cam.position.x,0,cam.position.z);dust.rotation.y+=dt*.03;netTick(dt);fxUpdate(dt);decUp(dt);ragUp(dt);grenUp(dt);P.blind=Math.max(0,(P.blind||0)-dt);$('white').style.opacity=Math.min(1,P.blind);hud()}
 if(P.alive||!running){cam.position.set(P.x,1.7+Math.sin(P.bt||0)*.035*(P.mv||0),P.z);cam.rotation.set(P.pitch,P.yaw,0)}
 else{const L=bots.filter(b=>b.alive&&b.team===P.team),t=L.length?L[((P.sp||0)%L.length+L.length)%L.length]:null;
  if(t){const ry=t.g.rotation.y;cam.position.set(t.x-Math.sin(ry)*3.2,2.4,t.z-Math.cos(ry)*3.2);cam.rotation.set(-.25,ry+Math.PI,0);if(G.ph==='live')say('Наблюдение: '+t.name+' (кнопка Смена)')}
  else{cam.position.set(P.x,.5,P.z);cam.rotation.set(P.pitch,P.yaw,.8)}}
 gunH.visible=P.alive;
 renderer.render(scene,cam)}
netInit();requestAnimationFrame(loop);
</script></body></html>
