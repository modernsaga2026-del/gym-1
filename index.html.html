import { useState, useEffect, useRef, useCallback, useMemo } from "react";
import { BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer, CartesianGrid } from "recharts";

/* ── TOKENS ── */
const C = { lime:"#C8FF00", cyan:"#00F5FF", orange:"#FF6B35", pink:"#FF3CAC", violet:"#7B2FFF" };

/* ── SAFE STORAGE — falls back gracefully if localStorage is unavailable ── */
const store = {
  get:(k,fb=null)=>{ try{ const v=localStorage.getItem(k); return v?JSON.parse(v):fb }catch{ return fb } },
  set:(k,v)=>{ try{ localStorage.setItem(k,JSON.stringify(v)) }catch{} },
  str:(k,fb="")=>{ try{ return localStorage.getItem(k)||fb }catch{ return fb } },
  sset:(k,v)=>{ try{ localStorage.setItem(k,v) }catch{} },
};

/* ── SPLITS ── */
const SPLITS = {
  PUSH:    {label:"PUSH",    sub:"Chest · Shoulder · Triceps", emoji:"💥", color:C.lime},
  PULL:    {label:"PULL",    sub:"Back · Biceps",               emoji:"🔗", color:C.cyan},
  LOWER:   {label:"LOWER",  sub:"Legs · Abs",                  emoji:"⚡", color:C.orange},
  CARDIO:  {label:"CARDIO", sub:"Treadmill",                   emoji:"🏃", color:C.pink},
  WELLNESS:{label:"WELLNESS",sub:"Yoga · Mobility",            emoji:"🧘", color:C.violet},
};

/* ── DEFAULT EXERCISES ── */
const DEF = {
  PUSH:[
    {id:"px0",name:"INCLINE BENCH PRESS",    sets:3,reps:10,unit:"lb"},
    {id:"px1",name:"FLAT DUMBBELL PRESS",     sets:3,reps:10,unit:"lb"},
    {id:"px2",name:"CABLE CHEST FLY",         sets:3,reps:12,unit:"lb"},
    {id:"px3",name:"DUMBBELL SHOULDER PRESS", sets:3,reps:10,unit:"lb"},
    {id:"px4",name:"SIDE LATERAL RAISE",      sets:3,reps:12,unit:"lb"},
    {id:"px5",name:"TRICEP ROPE PULLDOWN",    sets:3,reps:12,unit:"lb"},
    {id:"px6",name:"TRICEP MACHINE",          sets:3,reps:12,unit:"lb"},
  ],
  PULL:[
    {id:"bx0",name:"BARBELL ROW",      sets:3,reps:12,unit:"lb"},
    {id:"bx1",name:"LAT PULLDOWN",     sets:3,reps:12,unit:"lb"},
    {id:"bx2",name:"SEATED CABLE ROW", sets:3,reps:12,unit:"lb"},
    {id:"bx3",name:"BARBELL CURL",     sets:3,reps:10,unit:"lb"},
    {id:"bx4",name:"PREACHER CURL",    sets:3,reps:10,unit:"lb"},
    {id:"bx5",name:"HAMMER CURL",      sets:3,reps:12,unit:"lb"},
  ],
  LOWER:[
    {id:"lx0",name:"BARBELL SQUAT",     sets:3,reps:8, unit:"lb"},
    {id:"lx1",name:"LEG PRESS",         sets:3,reps:10,unit:"lb"},
    {id:"lx2",name:"LEG EXTENSION",     sets:3,reps:12,unit:"lb"},
    {id:"lx3",name:"LEG CURL",          sets:3,reps:12,unit:"lb"},
    {id:"lx4",name:"ROMANIAN DEADLIFT", sets:3,reps:12,unit:"lb"},
    {id:"lx5",name:"HANGING LEG RAISES",sets:3,reps:15,unit:"reps"},
  ],
  CARDIO:[],
  WELLNESS:[
    {id:"wx0",name:"SUN SALUTATION",   sets:3,reps:5,  unit:"rounds"},
    {id:"wx1",name:"WARRIOR SEQUENCE", sets:3,reps:5,  unit:"rounds"},
    {id:"wx2",name:"HIP FLEXOR HOLD",  sets:3,reps:60, unit:"sec"},
    {id:"wx3",name:"PIGEON POSE",      sets:3,reps:60, unit:"sec"},
  ],
};

const CARDIO_F=[
  {key:"duration",label:"DURATION",  unit:"min",  icon:"⏱"},
  {key:"distance",label:"DISTANCE",  unit:"km",   icon:"📏"},
  {key:"calories",label:"CALORIES",  unit:"kcal", icon:"🔥"},
  {key:"speed",   label:"AVG SPEED", unit:"km/h", icon:"💨"},
  {key:"incline", label:"INCLINE",   unit:"%",    icon:"⛰"},
  {key:"heart",   label:"HEART RATE",unit:"bpm",  icon:"❤"},
];

const todayISO=()=>new Date().toISOString().split("T")[0];
const fmtSecs=s=>`${String(Math.floor(s/3600)).padStart(2,"0")}:${String(Math.floor(s%3600/60)).padStart(2,"0")}:${String(s%60).padStart(2,"0")}`;
const fmtDT=iso=>{ try{ return new Date(iso).toLocaleString("en-US",{month:"short",day:"numeric",hour:"2-digit",minute:"2-digit"}) }catch{ return iso } };

/* ── CSS ── */
const CSS=`
@import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap');
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
input[type=number]::-webkit-inner-spin-button{opacity:.22}
::-webkit-scrollbar{width:3px;height:3px}
::-webkit-scrollbar-thumb{background:rgba(200,255,0,.25);border-radius:2px}
::placeholder{color:#333}
@keyframes a1{0%,100%{transform:translate(0,0) scale(1)}33%{transform:translate(70px,-50px) scale(1.12)}66%{transform:translate(-35px,70px) scale(.9)}}
@keyframes a2{0%,100%{transform:translate(0,0)}33%{transform:translate(-60px,45px) scale(1.15)}66%{transform:translate(80px,-60px) scale(.95)}}
@keyframes a3{0%,100%{transform:translate(0,0)}50%{transform:translate(45px,80px) scale(1.08)}}
@keyframes a4{0%,100%{transform:translate(0,0)}40%{transform:translate(-80px,-45px) scale(1.2)}80%{transform:translate(55px,35px) scale(.88)}}
@keyframes a5{0%,100%{transform:translate(0,0)}50%{transform:translate(60px,-70px) scale(1.25)}}
@keyframes spin{from{transform:rotate(0deg) scale(2)}to{transform:rotate(360deg) scale(2)}}
@keyframes rise{0%{transform:translateY(100vh) scale(0);opacity:0}10%{opacity:.8}90%{opacity:.3}100%{transform:translateY(-10px) scale(1);opacity:0}}
@keyframes gpulse{0%,100%{opacity:.28}50%{opacity:.55}}
@keyframes fadeUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.25}}
@keyframes slideIn{from{transform:translateX(-8px);opacity:0}to{transform:translateX(0);opacity:1}}

.glass{background:linear-gradient(145deg,rgba(255,255,255,.08),rgba(255,255,255,.025));backdrop-filter:blur(24px) saturate(1.5);border:1px solid rgba(255,255,255,.09);border-radius:18px;box-shadow:0 1px 0 rgba(255,255,255,.09) inset,0 -1px 0 rgba(0,0,0,.55) inset,0 18px 55px rgba(0,0,0,.5);position:relative;overflow:hidden;transition:transform .2s,box-shadow .2s}
.glass::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(255,255,255,.16),transparent)}
.lglass{background:rgba(5,2,15,.65);backdrop-filter:blur(12px);border-radius:8px;padding:3px 9px;display:inline-block}
.btn-lime{background:linear-gradient(135deg,#C8FF00,#8ab000);color:#000;border:none;border-radius:12px;font-family:'Syne',sans-serif;font-weight:800;letter-spacing:2px;cursor:pointer;box-shadow:0 4px 18px rgba(200,255,0,.3);transition:all .2s}
.btn-lime:hover{box-shadow:0 6px 26px rgba(200,255,0,.48);transform:translateY(-1px)}
.btn-ghost{background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.11);color:rgba(255,255,255,.7);border-radius:10px;cursor:pointer;font-family:'Syne',sans-serif;font-weight:600;letter-spacing:1px;transition:all .15s}
.btn-ghost:hover{background:rgba(255,255,255,.1);border-color:rgba(200,255,0,.3);color:#C8FF00}
.btn-ghost-on{background:rgba(200,255,0,.12)!important;border-color:rgba(200,255,0,.45)!important;color:#C8FF00!important}
.btn-start{background:linear-gradient(135deg,#00E676,#00b248);color:#000;border:none;border-radius:11px;font-family:'Syne',sans-serif;font-weight:800;letter-spacing:2px;cursor:pointer;box-shadow:0 4px 16px rgba(0,230,118,.3);transition:all .2s}
.btn-start:hover{box-shadow:0 6px 26px rgba(0,230,118,.48);transform:translateY(-1px)}
.btn-start:disabled{opacity:.38;cursor:not-allowed;transform:none!important}
.btn-end{background:linear-gradient(135deg,#FF3CAC,#c0006a);color:#fff;border:none;border-radius:11px;font-family:'Syne',sans-serif;font-weight:800;letter-spacing:2px;cursor:pointer;box-shadow:0 4px 16px rgba(255,60,172,.3);transition:all .2s}
.btn-end:hover{box-shadow:0 6px 26px rgba(255,60,172,.48);transform:translateY(-1px)}
.btn-end:disabled{opacity:.38;cursor:not-allowed;transform:none!important}
.pbar-track{background:rgba(255,255,255,.06);border-radius:100px;overflow:hidden}
.pbar-fill{height:100%;border-radius:100px;background:linear-gradient(90deg,#8ab000,#C8FF00);box-shadow:0 0 7px rgba(200,255,0,.5);transition:width .45s cubic-bezier(.4,0,.2,1)}
.num-in{background:rgba(0,0,0,.65);border:1px solid rgba(255,255,255,.07);border-bottom:1.5px solid rgba(200,255,0,.28);border-radius:7px 7px 0 0;color:#fff;outline:none;font-family:'DM Mono',monospace;text-align:center;transition:border-color .2s;width:100%}
.num-in:focus{border-bottom-color:#C8FF00;box-shadow:0 2px 0 rgba(200,255,0,.36)}
.thumb-sq{position:relative;border-radius:13px;overflow:hidden;background:rgba(0,0,0,.72);border:1.5px dashed rgba(255,255,255,.12);cursor:pointer;transition:border-color .2s;flex-shrink:0}
.thumb-sq:hover{border-color:rgba(200,255,0,.42)}
.thumb-ov{position:absolute;inset:0;background:rgba(0,0,0,.7);display:flex;align-items:center;justify-content:center;opacity:0;transition:opacity .2s}
.thumb-sq:hover .thumb-ov{opacity:1}
.chip{font-family:'DM Mono',monospace;font-size:10px;border-radius:100px;padding:4px 11px;letter-spacing:.8px;border:1px solid rgba(255,255,255,.09);background:rgba(255,255,255,.04);color:rgba(255,255,255,.5);cursor:pointer;transition:all .15s;white-space:nowrap}
.chip:hover{border-color:rgba(200,255,0,.3);color:#C8FF00}
.chip-on{background:rgba(200,255,0,.12)!important;border-color:rgba(200,255,0,.45)!important;color:#C8FF00!important}
.fadeup{animation:fadeUp .28s cubic-bezier(.4,0,.2,1) both}
.blink{animation:blink 1s ease-in-out infinite}
.lbl{font-family:'DM Mono',monospace;font-size:9px;letter-spacing:2.5px;color:rgba(255,255,255,.42);text-transform:uppercase}
`;

/* ── ANIMATED BACKGROUND ── */
function AnimBG({col}){
  const pts=[
    {l:"9%",d:"0s",dur:"9s",c:"rgba(200,255,0,.8)",s:3},
    {l:"25%",d:"2s",dur:"12s",c:"rgba(0,245,255,.75)",s:2},
    {l:"45%",d:"4s",dur:"8s",c:"rgba(255,60,172,.7)",s:4},
    {l:"62%",d:"1s",dur:"14s",c:"rgba(123,47,255,.75)",s:2},
    {l:"76%",d:"6s",dur:"11s",c:"rgba(255,107,53,.75)",s:3},
  ];
  return(
    <div style={{position:"fixed",inset:0,zIndex:0,pointerEvents:"none",overflow:"hidden",background:"#05020f"}}>
      <div style={{position:"absolute",inset:0,background:"radial-gradient(ellipse 80% 60% at 50% 0%,#1a0533,#05020f 70%)"}}/>
      <div style={{position:"absolute",top:"-10%",left:"-5%",width:500,height:500,borderRadius:"60% 40% 70% 30%/50% 60% 40% 50%",background:"radial-gradient(ellipse,rgba(200,255,0,.18),transparent 72%)",filter:"blur(60px)",animation:"a1 16s ease-in-out infinite"}}/>
      <div style={{position:"absolute",top:"20%",right:"-10%",width:460,height:460,borderRadius:"40% 60% 30% 70%/60% 40% 60% 40%",background:"radial-gradient(ellipse,rgba(0,245,255,.15),transparent 72%)",filter:"blur(65px)",animation:"a2 19s ease-in-out infinite"}}/>
      <div style={{position:"absolute",bottom:"10%",left:"8%",width:400,height:400,borderRadius:"70% 30% 50% 50%/40% 60% 40% 60%",background:"radial-gradient(ellipse,rgba(255,60,172,.14),transparent 72%)",filter:"blur(70px)",animation:"a3 22s ease-in-out infinite"}}/>
      <div style={{position:"absolute",top:"-20%",left:"-10%",width:550,height:550,borderRadius:"50%",background:`radial-gradient(circle,${col}28,transparent 65%)`,filter:"blur(72px)",transition:"background 1.3s ease",animation:"a1 14s ease-in-out infinite"}}/>
      <div style={{position:"absolute",bottom:"-15%",right:"-10%",width:600,height:600,borderRadius:"50%",background:`radial-gradient(circle,${col}18,transparent 65%)`,filter:"blur(88px)",transition:"background 1.3s ease",animation:"a2 18s ease-in-out infinite"}}/>
      <div style={{position:"absolute",top:"50%",left:"50%",width:1200,height:1200,transform:"translate(-50%,-50%)",background:"conic-gradient(from 0deg,transparent,rgba(200,255,0,.03) 45deg,transparent 90deg,rgba(0,245,255,.04) 135deg,transparent 180deg,rgba(255,60,172,.03) 225deg,transparent 270deg,rgba(255,107,53,.03) 315deg,transparent)",animation:"spin 40s linear infinite"}}/>
      <div style={{position:"absolute",inset:0,backgroundImage:"linear-gradient(135deg,rgba(255,255,255,.014) 1px,transparent 1px),linear-gradient(45deg,rgba(255,255,255,.014) 1px,transparent 1px)",backgroundSize:"48px 48px",animation:"gpulse 6s ease-in-out infinite"}}/>
      <div style={{position:"absolute",inset:0,backgroundImage:"radial-gradient(circle,rgba(255,255,255,.052) 1px,transparent 1px)",backgroundSize:"28px 28px",opacity:.4}}/>
      {pts.map((p,i)=><div key={i} style={{position:"absolute",bottom:0,left:p.l,width:p.s,height:p.s,borderRadius:"50%",background:p.c,boxShadow:`0 0 ${p.s*4}px ${p.c}`,animation:`rise ${p.dur} ${p.d} ease-in infinite`}}/>)}
      <div style={{position:"absolute",top:0,left:0,right:0,height:2,background:`linear-gradient(90deg,transparent,${C.violet}cc 20%,${C.cyan}ff 40%,${col}ff 60%,${C.pink}cc 80%,transparent)`,boxShadow:`0 0 22px ${col}88`,transition:"box-shadow 1.3s"}}/>
      <div style={{position:"absolute",inset:0,background:"radial-gradient(ellipse 100% 100% at 50% 50%,transparent 44%,rgba(5,2,15,.65) 100%)"}}/>
    </div>
  );
}

/* ── THUMBNAIL ── */
function Thumb({exId,size=88}){
  const key=`thumb_${exId}`;
  const [src,setSrc]=useState(()=>store.str(key,""));
  const ref=useRef();
  const pick=e=>{
    const f=e.target.files[0];if(!f)return;
    const r=new FileReader();
    r.onload=ev=>{store.sset(key,ev.target.result);setSrc(ev.target.result)};
    r.readAsDataURL(f);
  };
  return(
    <div className="thumb-sq" style={{width:size,height:size,minWidth:size}} onClick={()=>ref.current.click()}>
      {src
        ?<img src={src} alt="" style={{width:"100%",height:"100%",objectFit:"cover"}}/>
        :<div style={{display:"flex",flexDirection:"column",alignItems:"center",justifyContent:"center",height:"100%",gap:5}}>
          <svg width="26" height="26" viewBox="0 0 32 32" fill="none">
            <rect x="2" y="6" width="28" height="20" rx="3" stroke="rgba(255,255,255,.2)" strokeWidth="1.5" fill="none"/>
            <circle cx="11" cy="13" r="3" stroke="rgba(255,255,255,.15)" strokeWidth="1.5" fill="none"/>
            <path d="M2 22l7-7 5 5 5-5 8 8" stroke="rgba(255,255,255,.15)" strokeWidth="1.5" strokeLinejoin="round" fill="none"/>
          </svg>
          <span style={{fontSize:8,color:"rgba(255,255,255,.28)",fontFamily:"'DM Mono',monospace",textAlign:"center",lineHeight:1.4}}>TAP TO<br/>ADD PHOTO</span>
        </div>}
      <div className="thumb-ov"><span style={{fontSize:22}}>📷</span></div>
      <input ref={ref} type="file" accept="image/*" style={{display:"none"}} onChange={pick}/>
    </div>
  );
}

/* ── MINI BAR CHART for exercise progress ── */
function ExChart({exName,color,history}){
  // history is passed as prop from root state — no direct LS access
  const [range,setRange]=useState("30D");
  const data=useMemo(()=>{
    const days=range==="7D"?7:range==="30D"?30:3650;
    const cut=Date.now()-days*86400000;
    const map={};
    history.filter(l=>l.exName===exName&&new Date(l.date).getTime()>=cut)
      .forEach(l=>{if(!map[l.date]||l.maxW>map[l.date].w)map[l.date]={w:l.maxW,d:l.date.slice(5)}});
    return Object.values(map).sort((a,b)=>a.d.localeCompare(b.d));
  },[history,exName,range]);

  const Tip=({active,payload,label})=>{
    if(!active||!payload?.length)return null;
    return(
      <div style={{background:"rgba(5,2,15,.95)",border:`1px solid ${color}55`,borderRadius:10,padding:"8px 12px",fontFamily:"'DM Mono',monospace",fontSize:11}}>
        <div style={{color:"rgba(255,255,255,.45)",marginBottom:3}}>{label}</div>
        {payload.map((p,i)=><div key={i} style={{color:p.color}}>{p.name}: <span style={{color:"#fff"}}>{p.value}</span></div>)}
      </div>
    );
  };

  return(
    <div>
      <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:10}}>
        <div style={{fontWeight:800,fontSize:12,color:"#fff",letterSpacing:1}}>PROGRESS <span style={{color}}>CHART</span></div>
        <div style={{display:"flex",gap:4}}>
          {["7D","30D","ALL"].map(r=>(
            <button key={r} className={`chip ${range===r?"chip-on":""}`} style={{fontSize:9,padding:"3px 10px"}} onClick={()=>setRange(r)}>{r}</button>
          ))}
        </div>
      </div>
      {data.length===0
        ?<div style={{height:90,display:"flex",alignItems:"center",justifyContent:"center",color:"rgba(255,255,255,.18)",fontFamily:"'DM Mono',monospace",fontSize:10,letterSpacing:1}}>SAVE A SESSION TO SEE PROGRESS</div>
        :<ResponsiveContainer width="100%" height={110}>
          <BarChart data={data} margin={{top:4,right:4,bottom:0,left:-22}}>
            <CartesianGrid strokeDasharray="3 3" stroke="rgba(255,255,255,.04)" vertical={false}/>
            <XAxis dataKey="d" tick={{fill:"rgba(255,255,255,.32)",fontSize:9,fontFamily:"'DM Mono',monospace"}} axisLine={false} tickLine={false}/>
            <YAxis tick={{fill:"rgba(255,255,255,.32)",fontSize:9,fontFamily:"'DM Mono',monospace"}} axisLine={false} tickLine={false}/>
            <Tooltip content={<Tip/>}/>
            <Bar dataKey="w" name="Max Wt" fill={color} radius={[4,4,0,0]}/>
          </BarChart>
        </ResponsiveContainer>}
    </div>
  );
}

/* ── EXERCISE CARD ── */
function ExCard({ex,color,savedSets,onSets,onEx,onDelete,prev,history}){
  const [open,setOpen]=useState(false);
  const [showChart,setShowChart]=useState(false);
  const sets=savedSets&&savedSets.length>0?savedSets:Array.from({length:3},()=>({weight:"",reps:""}));
  const logged=sets.filter(s=>s.weight||s.reps).length;
  const pct=sets.length>0?Math.round(logged/sets.length*100):0;
  const done=logged===sets.length&&sets.length>0;
  const upd=(i,field,val)=>{const ns=[...sets];ns[i]={...ns[i],[field]:val};onSets(ns)};
  const targetLine=prev
    ?`${sets.length} SETS · TARGET: ${prev.weight}${ex.unit} × ${prev.reps}`
    :`${sets.length} SETS · ${ex.reps} REPS · ${ex.unit}`;

  return(
    <div className="glass" style={{marginBottom:12,borderColor:done?`${color}55`:"rgba(255,255,255,.08)",background:done?`${color}09`:undefined}}>
      {/* photo left | info right */}
      <div style={{display:"flex",gap:12,padding:"12px 12px 0"}}>
        <Thumb exId={ex.id} size={88}/>
        <div style={{flex:1,minWidth:0,display:"flex",flexDirection:"column",gap:5}}>
          <input value={ex.name} onChange={e=>onEx({...ex,name:e.target.value.toUpperCase()})}
            style={{background:"rgba(0,0,0,.5)",border:"none",borderBottom:`1.5px solid ${color}44`,color:"#fff",fontSize:13,fontFamily:"'Syne',sans-serif",fontWeight:800,letterSpacing:1.5,outline:"none",width:"100%",paddingBottom:3,transition:"border-color .2s",borderRadius:0,whiteSpace:"normal",wordBreak:"break-word",lineHeight:1.35}}
            onFocus={e=>e.target.style.borderBottomColor=color}
            onBlur={e=>e.target.style.borderBottomColor=`${color}44`}/>

          {prev
            ?<div style={{display:"inline-flex",alignItems:"center",flexWrap:"wrap",gap:5,background:"rgba(0,0,0,.55)",border:`1px solid ${color}30`,borderRadius:6,padding:"3px 8px",width:"fit-content"}}>
              <span style={{fontSize:8,color:"rgba(255,255,255,.4)",fontFamily:"'DM Mono',monospace",letterSpacing:1}}>LAST TIME</span>
              <span style={{fontSize:11,color,fontFamily:"'DM Mono',monospace",fontWeight:500}}>{prev.weight}{ex.unit} · {prev.reps}×{prev.sets}</span>
              <span style={{fontSize:8,color:"rgba(255,255,255,.22)",fontFamily:"'DM Mono',monospace"}}>{prev.date}</span>
            </div>
            :<div style={{fontSize:9,color:"rgba(255,255,255,.22)",fontFamily:"'DM Mono',monospace",letterSpacing:.8}}>NO PREVIOUS RECORD</div>}

          <div style={{display:"flex",alignItems:"center",gap:4,marginTop:1,flexWrap:"wrap"}}>
            <div style={{fontSize:9,color:"rgba(255,255,255,.38)",fontFamily:"'DM Mono',monospace",letterSpacing:.5,flex:1,minWidth:0,wordBreak:"break-word"}}>{targetLine}</div>
            <div style={{display:"flex",alignItems:"center",gap:4,flexShrink:0}}>
              <span style={{fontFamily:"'DM Mono',monospace",fontSize:12,fontWeight:500,color:done?color:"rgba(255,255,255,.38)"}}>{pct}%</span>
              <button className="btn-ghost" style={{padding:"4px 8px",fontSize:11,lineHeight:1,transform:open?"rotate(180deg)":"none",transition:"transform .2s"}} onClick={()=>setOpen(!open)}>▾</button>
              <button className={`btn-ghost ${showChart?"btn-ghost-on":""}`} style={{padding:"4px 7px",fontSize:11}} onClick={()=>setShowChart(!showChart)}>📊</button>
              <button onClick={onDelete} title="Delete exercise"
                style={{background:"transparent",border:"none",color:"rgba(255,80,80,.45)",cursor:"pointer",fontSize:14,padding:"4px 5px",lineHeight:1,transition:"color .15s"}}
                onMouseEnter={e=>e.currentTarget.style.color="rgba(255,80,80,.9)"}
                onMouseLeave={e=>e.currentTarget.style.color="rgba(255,80,80,.45)"}>🗑</button>
            </div>
          </div>
          <div className="pbar-track" style={{height:3}}>
            <div className="pbar-fill" style={{width:`${pct}%`,background:done?color:`${color}88`}}/>
          </div>
        </div>
      </div>

      {open&&(
        <div style={{padding:"10px 12px 12px",display:"flex",flexDirection:"column",gap:7}}>
          <div className="lbl" style={{marginBottom:4,color:"rgba(255,255,255,.5)"}}>SETS</div>
          {sets.map((s,i)=>(
            <div key={i} style={{display:"grid",gridTemplateColumns:"26px 1fr 1fr 28px",gap:6,alignItems:"center",background:"rgba(0,0,0,.55)",border:"1px solid rgba(255,255,255,.06)",borderRadius:10,padding:"8px 10px"}}>
              <span style={{fontFamily:"'DM Mono',monospace",fontSize:11,fontWeight:500,color,textAlign:"center"}}>{String(i+1).padStart(2,"0")}</span>
              {[["WT",ex.unit,s.weight,"weight"],["REPS","×",s.reps,"reps"]].map(([lbl,ph,val,field])=>(
                <div key={field}>
                  <div style={{fontSize:8,color:"rgba(255,255,255,.34)",letterSpacing:1,fontFamily:"'DM Mono',monospace",marginBottom:3,textAlign:"center"}}>{lbl} ({ph})</div>
                  <input type="number" value={val} placeholder="—" className="num-in" style={{fontSize:18,fontWeight:700,padding:"5px 4px"}} onChange={e=>upd(i,field,e.target.value)}/>
                </div>
              ))}
              <button onClick={()=>sets.length>1&&onSets(sets.filter((_,j)=>j!==i))}
                style={{background:"transparent",border:"none",color:sets.length>1?"rgba(255,80,80,.55)":"rgba(255,255,255,.1)",cursor:sets.length>1?"pointer":"not-allowed",fontSize:16,paddingTop:12,transition:"color .15s"}}
                onMouseEnter={e=>{if(sets.length>1)e.currentTarget.style.color="rgba(255,80,80,.9)"}}
                onMouseLeave={e=>{if(sets.length>1)e.currentTarget.style.color="rgba(255,80,80,.55)"}}>×</button>
            </div>
          ))}
          <div style={{display:"flex",gap:6,marginTop:4}}>
            <button className="btn-ghost" style={{flex:1,padding:"8px",fontSize:11,letterSpacing:1}} onClick={()=>onSets([...sets,{weight:"",reps:""}])}>+ SET</button>
            {prev&&<button className="btn-ghost" style={{flex:1,padding:"8px",fontSize:11,letterSpacing:1,color:"rgba(200,255,0,.75)",borderColor:"rgba(200,255,0,.22)"}} onClick={()=>onSets(sets.map(()=>({weight:prev.weight,reps:prev.reps})))}>↩ FILL LAST</button>}
          </div>
          <textarea placeholder="Notes…" value={ex.notes||""} onChange={e=>onEx({...ex,notes:e.target.value})} rows={2}
            style={{background:"rgba(0,0,0,.5)",border:"1px solid rgba(255,255,255,.06)",borderRadius:8,color:"rgba(255,255,255,.72)",fontSize:11,padding:"8px 10px",resize:"none",outline:"none",fontFamily:"'DM Mono',monospace",marginTop:4}}
            onFocus={e=>{e.target.style.borderColor=`${color}30`}}
            onBlur={e=>{e.target.style.borderColor="rgba(255,255,255,.06)"}}/>
        </div>
      )}

      {showChart&&(
        <div style={{padding:"0 12px 12px",borderTop:"1px solid rgba(255,255,255,.05)"}}>
          <ExChart exName={ex.name} color={color} history={history}/>
        </div>
      )}
    </div>
  );
}

/* ── CARDIO PANEL ── */
function CardioPanel({data,onChange,color}){
  const pace=(data.distance>0&&data.duration>0)?(data.duration/data.distance).toFixed(1):null;
  const cpk=(data.distance>0&&data.calories>0)?Math.round(data.calories/data.distance):null;
  return(
    <div>
      <div className="glass" style={{padding:"14px",marginBottom:12,background:`${color}12`,borderColor:`${color}33`}}>
        <div style={{fontFamily:"'Syne',sans-serif",fontWeight:900,fontSize:20,letterSpacing:3,color}}>🏃 TREADMILL</div>
        <div className="lbl" style={{marginTop:3,color:"rgba(255,255,255,.5)"}}>LOG CARDIO METRICS</div>
      </div>
      <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:10,marginBottom:12}}>
        {CARDIO_F.map(f=>(
          <div key={f.key} className="glass" style={{padding:"12px 13px"}}>
            <div style={{fontSize:14,marginBottom:4}}>{f.icon}</div>
            <div className="lbl" style={{marginBottom:5,color:"rgba(255,255,255,.55)"}}>{f.label}</div>
            <div style={{display:"flex",alignItems:"baseline",gap:4}}>
              <input type="number" value={data[f.key]||""} placeholder="0" onChange={e=>onChange(f.key,e.target.value)}
                style={{background:"transparent",border:"none",borderBottom:`1.5px solid ${color}55`,color:"#fff",fontSize:26,fontFamily:"'Syne',sans-serif",fontWeight:800,outline:"none",width:"100%",padding:"2px 0"}}
                onFocus={e=>e.target.style.borderBottomColor=color}
                onBlur={e=>e.target.style.borderBottomColor=`${color}55`}/>
              <span style={{fontSize:9,color:"rgba(255,255,255,.38)",whiteSpace:"nowrap",fontFamily:"'DM Mono',monospace"}}>{f.unit}</span>
            </div>
          </div>
        ))}
      </div>
      {(pace||cpk)&&(
        <div className="glass" style={{padding:"12px 15px",marginBottom:12,borderColor:`${color}44`,background:`${color}0a`}}>
          <div className="lbl" style={{color,marginBottom:8}}>⚡ AUTO-CALCULATED</div>
          <div style={{display:"flex",gap:22}}>
            {pace&&<div><div className="lbl" style={{marginBottom:3,color:"rgba(255,255,255,.5)"}}>PACE</div><div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:26,color}}>{pace}<span style={{fontSize:11}}> min/km</span></div></div>}
            {cpk&&<div><div className="lbl" style={{marginBottom:3,color:"rgba(255,255,255,.5)"}}>CAL/KM</div><div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:26,color}}>{cpk}<span style={{fontSize:11}}> kcal</span></div></div>}
          </div>
        </div>
      )}
      <div className="glass" style={{padding:"12px 15px"}}>
        <div className="lbl" style={{marginBottom:7,color:"rgba(255,255,255,.55)"}}>SESSION NOTES</div>
        <textarea placeholder="Intervals, incline changes, how it felt…" value={data.notes||""} onChange={e=>onChange("notes",e.target.value)} rows={3}
          style={{width:"100%",background:"transparent",border:"none",color:"rgba(255,255,255,.72)",fontSize:12,outline:"none",resize:"none",fontFamily:"'DM Mono',monospace"}}/>
      </div>
    </div>
  );
}

/* ── ANALYTICS — receives savedHistory and logs as props, no direct LS access ── */
function Analytics({logs,exercises,savedHistory}){
  const [catF,setCatF]=useState("ALL");
  const [range,setRange]=useState("ALL");
  const [sort,setSort]=useState("NEWEST");
  const [search,setSearch]=useState("");
  const [exp,setExp]=useState(null);
  const today=todayISO();

  // Derive unique saved dates purely from the savedHistory prop (React state, always fresh)
  const savedDates=useMemo(()=>[...new Set(savedHistory.map(h=>h.date))],[savedHistory]);

  const filtered=useMemo(()=>{
    const days=range==="7D"?7:range==="30D"?30:99999;
    const cut=Date.now()-days*86400000;
    return savedDates
      .filter(d=>{
        const dw=Object.keys(logs[d]||{}).filter(k=>!k.startsWith("_"));
        return(
          new Date(d).getTime()>=cut
          &&(catF==="ALL"||dw.includes(catF))
          &&(!search||(d.includes(search)||dw.some(c=>c.toLowerCase().includes(search.toLowerCase()))))
        );
      })
      .sort((a,b)=>
        sort==="NEWEST"?b.localeCompare(a):
        sort==="OLDEST"?a.localeCompare(b):
        Object.keys(logs[b]||{}).length-Object.keys(logs[a]||{}).length
      );
  },[savedDates,logs,catF,range,sort,search]);

  // Aggregate stats only from saved sessions
  let totSets=0,totMins=0,totCals=0,totKm=0;
  const catCnt={};
  filtered.forEach(d=>{
    Object.entries(logs[d]||{}).filter(([k])=>!k.startsWith("_")).forEach(([cat,data])=>{
      catCnt[cat]=(catCnt[cat]||0)+1;
      if(cat==="CARDIO"&&data.cardio){
        totMins+=+data.cardio.duration||0;
        totCals+=+data.cardio.calories||0;
        totKm+=+data.cardio.distance||0;
      } else {
        Object.values(data).forEach(v=>{if(Array.isArray(v))totSets+=v.filter(s=>s.weight||s.reps).length});
      }
    });
  });
  const favCat=Object.entries(catCnt).sort((a,b)=>b[1]-a[1])[0];

  // Weekly bar chart — only count saved dates
  const last7=Array.from({length:7},(_,i)=>{
    const d=new Date();d.setDate(d.getDate()-6+i);
    const k=d.toISOString().split("T")[0];
    const n=savedDates.includes(k)?Object.keys(logs[k]||{}).filter(x=>!x.startsWith("_")).length:0;
    return{k,dow:d.toLocaleDateString("en-US",{weekday:"short"}).slice(0,2).toUpperCase(),n};
  });

  const stats=[
    {l:"SESSIONS",  v:filtered.length,      u:"total", ico:"📅",c:C.lime},
    {l:"SETS",      v:totSets,              u:"logged", ico:"💪",c:C.cyan},
    {l:"CARDIO",    v:Math.round(totMins),  u:"min",    ico:"🏃",c:C.pink},
    {l:"CALORIES",  v:Math.round(totCals),  u:"kcal",   ico:"🔥",c:C.orange},
    {l:"KM",        v:totKm.toFixed(1),     u:"run",    ico:"📏",c:C.violet},
    {l:"TOP SPLIT", v:favCat?favCat[0].split(" ")[0]:"—", u:favCat?`${favCat[1]}×`:"", ico:"⭐",c:"#FFD700"},
  ];

  return(
    <div style={{padding:"14px 14px 0"}}>
      {/* Search */}
      <div className="glass" style={{padding:"10px 14px",marginBottom:10,display:"flex",alignItems:"center",gap:8}}>
        <span style={{fontSize:14,color:"rgba(255,255,255,.4)"}}>⌕</span>
        <input value={search} onChange={e=>setSearch(e.target.value)} placeholder="Search date or category…"
          style={{flex:1,background:"transparent",border:"none",color:"#fff",fontSize:13,outline:"none",fontFamily:"'DM Mono',monospace"}}/>
      </div>

      {/* Range + sort filters */}
      <div style={{display:"flex",gap:5,marginBottom:8,overflowX:"auto",paddingBottom:2}}>
        {[{l:"ALL",v:"ALL"},{l:"7D",v:"7D"},{l:"30D",v:"30D"}].map(r=>(
          <button key={r.v} className={`chip ${range===r.v?"chip-on":""}`} onClick={()=>setRange(r.v)}>{r.l}</button>
        ))}
        <div style={{width:1,background:"rgba(255,255,255,.08)",flexShrink:0,margin:"0 4px"}}/>
        {["NEWEST","OLDEST"].map(s=>(
          <button key={s} className={`chip ${sort===s?"chip-on":""}`} onClick={()=>setSort(s)}>{s}</button>
        ))}
      </div>

      {/* Category filters */}
      <div style={{display:"flex",gap:5,marginBottom:14,overflowX:"auto",paddingBottom:2}}>
        {["ALL",...Object.keys(SPLITS)].map(c=>{
          const col=SPLITS[c]?.color||C.lime;const active=catF===c;
          return(
            <button key={c} className={`chip ${active?"chip-on":""}`} style={active?{background:`${col}18`,borderColor:col,color:col}:{}} onClick={()=>setCatF(c)}>
              {c==="ALL"?"⚡ ALL":`${SPLITS[c].emoji} ${c}`}
            </button>
          );
        })}
      </div>

      {/* Stat tiles */}
      <div style={{display:"grid",gridTemplateColumns:"repeat(3,1fr)",gap:8,marginBottom:14}}>
        {stats.map(s=>(
          <div key={s.l} className="glass" style={{padding:"12px 8px",textAlign:"center"}}>
            <div style={{fontSize:18,marginBottom:3}}>{s.ico}</div>
            <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:22,color:s.c,lineHeight:1,textShadow:`0 0 14px ${s.c}44`}}>{s.v}</div>
            <div style={{fontSize:8,color:"rgba(255,255,255,.35)",fontFamily:"'DM Mono',monospace",letterSpacing:.8,marginTop:2}}>{s.u}</div>
            <div style={{fontSize:7,color:"rgba(255,255,255,.2)",fontFamily:"'DM Mono',monospace",letterSpacing:.8,marginTop:1}}>{s.l}</div>
          </div>
        ))}
      </div>

      {/* Weekly bar */}
      <div className="glass" style={{padding:"14px 16px",marginBottom:14}}>
        <div className="lbl" style={{marginBottom:12,color:"rgba(255,255,255,.55)"}}>WEEKLY FREQUENCY</div>
        <div style={{display:"flex",gap:6,alignItems:"flex-end",height:52}}>
          {last7.map(({k,dow,n})=>(
            <div key={k} style={{flex:1,display:"flex",flexDirection:"column",alignItems:"center",gap:4}}>
              <div style={{width:"100%",borderRadius:"4px 4px 2px 2px",height:n>0?Math.max(8,n*16):4,background:n>0?"linear-gradient(180deg,#C8FF00,#8ab000)":"rgba(255,255,255,.05)",boxShadow:n>0?"0 0 9px rgba(200,255,0,.4)":"none",transition:"height .4s"}}/>
              <div style={{fontSize:8,color:k===today?"#fff":"rgba(255,255,255,.32)",fontFamily:"'DM Mono',monospace",fontWeight:k===today?700:400}}>{dow}</div>
            </div>
          ))}
        </div>
      </div>

      {/* Session list */}
      <div className="lbl" style={{marginBottom:10,color:"rgba(255,255,255,.42)"}}>
        {filtered.length} SESSION{filtered.length!==1?"S":""}
      </div>

      {filtered.length===0
        ?<div className="glass" style={{padding:"40px 20px",textAlign:"center"}}>
          <div style={{fontSize:40,marginBottom:10}}>📋</div>
          <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:16,letterSpacing:2,color:"rgba(255,255,255,.28)"}}>
            {savedHistory.length===0?"SAVE A SESSION TO SEE ANALYTICS":"NO SESSIONS MATCH FILTER"}
          </div>
        </div>
        :filtered.map(date=>{
          const dl=logs[date]||{};
          const dw=Object.keys(dl).filter(k=>!k.startsWith("_"));
          const isToday=date===today;
          const isOpen=exp===date;
          const dur=dl._meta?.duration;
          return(
            <div key={date} className="glass" style={{marginBottom:10,overflow:"hidden",borderLeft:`2px solid ${isToday?C.lime:"rgba(255,255,255,.06)"}`}}>
              <div onClick={()=>setExp(isOpen?null:date)} style={{display:"flex",alignItems:"center",padding:"13px 14px",cursor:"pointer",gap:10}}>
                <div style={{flex:1}}>
                  <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:14,letterSpacing:1.5,color:"#fff",display:"flex",alignItems:"center",gap:8}}>
                    {new Date(date+"T00:00:00").toLocaleDateString("en-US",{weekday:"short",month:"short",day:"numeric"}).toUpperCase()}
                    {isToday&&<span style={{background:"rgba(200,255,0,.12)",border:"1px solid rgba(200,255,0,.35)",borderRadius:100,padding:"2px 8px",fontSize:8,color:C.lime,fontFamily:"'DM Mono',monospace",letterSpacing:1}}>TODAY</span>}
                  </div>
                  <div className="lbl" style={{marginTop:3,color:"rgba(255,255,255,.4)"}}>
                    {dw.length} SPLIT{dw.length!==1?"S":""}{dur?` · ${dur}min`:""}
                  </div>
                </div>
                <div style={{display:"flex",gap:4}}>
                  {dw.map(d=><span key={d} style={{fontSize:18,filter:`drop-shadow(0 0 5px ${SPLITS[d]?.color||"#fff"}aa)`}}>{SPLITS[d]?.emoji||"🏋️"}</span>)}
                </div>
                <span style={{color:"rgba(255,255,255,.3)",fontSize:14,transform:isOpen?"rotate(180deg)":"none",transition:"transform .2s"}}>▾</span>
              </div>
              {isOpen&&(
                <div style={{padding:"0 14px 14px",borderTop:"1px solid rgba(255,255,255,.05)"}}>
                  {dw.map(cat=>{
                    const col=SPLITS[cat]?.color||C.lime;const ed=dl[cat]||{};
                    return(
                      <div key={cat} style={{marginTop:14}}>
                        <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:12,letterSpacing:2,color:col,marginBottom:8}}>{SPLITS[cat]?.emoji} {cat}</div>
                        {cat==="CARDIO"&&ed.cardio
                          ?<div style={{display:"flex",gap:6,flexWrap:"wrap"}}>
                            {[["⏱",ed.cardio.duration,"min"],["📏",ed.cardio.distance,"km"],["🔥",ed.cardio.calories,"kcal"],["💨",ed.cardio.speed,"km/h"]].map(([ic,v,u])=>
                              v?<div key={u} className="glass" style={{padding:"7px 11px",textAlign:"center",minWidth:56}}>
                                <div style={{fontSize:13}}>{ic}</div>
                                <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:17,color:col}}>{v}</div>
                                <div style={{fontSize:8,color:"rgba(255,255,255,.4)"}}>{u}</div>
                              </div>:null
                            )}
                          </div>
                          :<div style={{display:"flex",flexDirection:"column",gap:4}}>
                            {Object.entries(ed).filter(([k])=>!isNaN(k)).map(([i,sets])=>{
                              if(!Array.isArray(sets)||!sets.some(s=>s.weight||s.reps))return null;
                              const exList=exercises[cat]||DEF[cat]||[];
                              const nm=exList[+i]?.name||`Exercise ${+i+1}`;
                              const valid=sets.filter(s=>s.weight||s.reps);
                              return(
                                <div key={i} style={{background:"rgba(0,0,0,.45)",borderRadius:8,padding:"7px 12px",display:"flex",justifyContent:"space-between",alignItems:"center",border:"1px solid rgba(255,255,255,.04)"}}>
                                  <span style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"rgba(255,255,255,.45)",letterSpacing:.8,flex:1,minWidth:0,marginRight:8,wordBreak:"break-word"}}>{nm}</span>
                                  <span style={{fontFamily:"'DM Mono',monospace",fontSize:12,color:col,fontWeight:500,flexShrink:0}}>{valid.map(s=>`${s.weight||0}lb×${s.reps||0}`).join(" ")}</span>
                                </div>
                              );
                            })}
                          </div>
                        }
                      </div>
                    );
                  })}
                </div>
              )}
            </div>
          );
        })}
    </div>
  );
}

/* ══════════════════════════════════════════════════
   ROOT APP
══════════════════════════════════════════════════ */
export default function App(){
  const [view,setView]=useState("log");
  const [activeSplit,setActiveSplit]=useState(null);
  const [userName,setUserName]=useState(()=>store.str("il_name","ATHLETE"));
  const [editName,setEditName]=useState(false);
  const [exercises,setExercises]=useState(()=>store.get("il_ex_v8",DEF));
  const [logs,setLogs]=useState(()=>store.get("il_logs_v8",{}));
  // savedHistory lives in React state — single source of truth for Analytics
  const [savedHistory,setSavedHistory]=useState(()=>store.get("il_saved_v8",[])||[]);
  const [savedMsg,setSavedMsg]=useState(false);
  // Timer state
  const [workoutOn,setWorkoutOn]=useState(false);
  const [startTime,setStartTime]=useState(null);
  const [elapsed,setElapsed]=useState(0);
  const [endTime,setEndTime]=useState(null);
  const [workoutName,setWorkoutName]=useState(()=>store.str("il_wname","MY WORKOUT"));
  const timerRef=useRef(null);
  const today=todayISO();

  useEffect(()=>{ store.set("il_ex_v8",exercises) },[exercises]);

  // Timer ticks using wall-clock diff — never drifts
  useEffect(()=>{
    clearInterval(timerRef.current);
    if(workoutOn&&startTime&&!endTime){
      timerRef.current=setInterval(()=>{
        setElapsed(Math.floor((Date.now()-new Date(startTime).getTime())/1000));
      },1000);
    }
    return()=>clearInterval(timerRef.current);
  },[workoutOn,startTime,endTime]);

  const splitColor=activeSplit?SPLITS[activeSplit].color:C.lime;

  /* ── START: only on manual button tap ── */
  const handleStart=()=>{
    const now=new Date().toISOString();
    setStartTime(now);setWorkoutOn(true);setEndTime(null);setElapsed(0);
    setLogs(prev=>{
      const u={...prev,[today]:{...(prev[today]||{}),_meta:{...(prev[today]?._meta||{}),startTime:now,endTime:null,duration:null}}};
      store.set("il_logs_v8",u);return u;
    });
  };

  /* ── END: freeze immediately ── */
  const handleEnd=()=>{
    clearInterval(timerRef.current);timerRef.current=null;
    const frozenElapsed=startTime?Math.floor((Date.now()-new Date(startTime).getTime())/1000):elapsed;
    setElapsed(frozenElapsed);
    const now=new Date().toISOString();
    const durMins=Math.round(frozenElapsed/60);
    setEndTime(now);setWorkoutOn(false);
    setLogs(prev=>{
      const u={...prev,[today]:{...(prev[today]||{}),_meta:{...(prev[today]?._meta||{}),endTime:now,duration:durMins}}};
      store.set("il_logs_v8",u);return u;
    });
  };

  /* ── SELECT SPLIT: no timer auto-start ── */
  const handleSplit=split=>{
    setActiveSplit(split);
    setLogs(prev=>{
      const u={...prev,[today]:{...(prev[today]||{}),[split]:{...(prev[today]?.[split]||{}),_start:new Date().toISOString()}}};
      store.set("il_logs_v8",u);return u;
    });
  };

  const getPrev=useCallback((split,idx)=>{
    const nm=exercises[split]?.[idx]?.name;if(!nm)return null;
    const past=Object.keys(logs).filter(d=>d!==today&&!d.startsWith("_")).sort().reverse();
    for(const d of past){
      const sets=logs[d]?.[split]?.[idx];
      if(Array.isArray(sets)&&sets.some(s=>s.weight||s.reps)){
        const v=sets.filter(s=>s.weight||s.reps);
        return{
          weight:(v.reduce((a,s)=>a+(+s.weight||0),0)/v.length).toFixed(1),
          reps:Math.round(v.reduce((a,s)=>a+(+s.reps||0),0)/v.length),
          sets:v.length,date:d.slice(5)
        };
      }
    }
    return null;
  },[logs,exercises,today]);

  /* Live sets — writes only to logs, NEVER to history */
  const updateSets=(split,idx,sets)=>{
    setLogs(prev=>{
      const td={...(prev[today]||{})};
      td[split]={...(td[split]||{}),[idx]:sets};
      const u={...prev,[today]:td};
      store.set("il_logs_v8",u);
      return u;
    });
  };

  const updateCardio=(key,val)=>{
    setLogs(prev=>{
      const u={...prev,[today]:{...(prev[today]||{}),CARDIO:{...(prev[today]?.CARDIO||{}),cardio:{...(prev[today]?.CARDIO?.cardio||{}),[key]:val}}}};
      store.set("il_logs_v8",u);return u;
    });
  };

  /* ── SAVE: only here do we commit to savedHistory ── */
  const handleSave=()=>{
    store.set("il_logs_v8",logs);
    const hist=[...savedHistory];
    const td=logs[today]||{};

    Object.entries(td).filter(([k])=>!k.startsWith("_")).forEach(([split,data])=>{
      if(split==="CARDIO"){
        if(data.cardio?.distance){
          const ei=hist.findIndex(h=>h.date===today&&h.exName==="__CARDIO_KM__");
          const entry={date:today,exName:"__CARDIO_KM__",maxW:+data.cardio.distance,vol:+data.cardio.distance};
          if(ei>=0)hist[ei]=entry;else hist.push(entry);
        }
      } else {
        (exercises[split]||[]).forEach((ex,i)=>{
          const sets=data[i];
          if(Array.isArray(sets)&&sets.some(s=>s.weight||s.reps)){
            const v=sets.filter(s=>s.weight||s.reps);
            const maxW=Math.max(...v.map(s=>+s.weight||0));
            const vol=v.reduce((a,s)=>a+(+s.weight||0)*(+s.reps||0),0);
            const ei=hist.findIndex(h=>h.date===today&&h.exName===ex.name);
            const entry={date:today,exName:ex.name,maxW,vol};
            if(ei>=0)hist[ei]=entry;else hist.push(entry);
          }
        });
      }
    });

    const trimmed=hist.slice(-2000);
    setSavedHistory(trimmed);          // update React state → Analytics re-renders
    store.set("il_saved_v8",trimmed); // persist for next session
    setSavedMsg(true);
    setTimeout(()=>setSavedMsg(false),2400);
  };

  const updateExMeta=(split,idx,ex)=>{
    setExercises(prev=>{const u={...prev,[split]:[...prev[split]]};u[split][idx]=ex;return u});
  };
  const deleteExercise=(split,idx)=>{
    setExercises(prev=>({...prev,[split]:prev[split].filter((_,i)=>i!==idx)}));
  };

  const getProgress=split=>{
    const exList=exercises[split]||[];if(!exList.length)return 0;
    const total=exList.length*3;
    const done=exList.reduce((acc,ex,i)=>{
      const s=logs[today]?.[split]?.[i];
      return acc+(Array.isArray(s)?s.filter(x=>x.weight||x.reps).length:0);
    },0);
    return total>0?Math.round(done/total*100):0;
  };

  const meta=logs[today]?._meta||{};
  const timerRunning=workoutOn&&!endTime;

  return(
    <div style={{minHeight:"100vh",background:"transparent",color:"#fff",maxWidth:480,margin:"0 auto",paddingBottom:100,fontFamily:"'Syne',sans-serif",position:"relative"}}>
      <style>{CSS}</style>
      <AnimBG col={splitColor}/>

      {/* ══ HEADER ══ */}
      <div style={{position:"sticky",top:0,zIndex:300,background:"rgba(5,2,15,.82)",backdropFilter:"blur(30px)",borderBottom:"1px solid rgba(255,255,255,.07)",padding:"10px 14px"}}>
        {/* Timer — prominent at top */}
        <div style={{textAlign:"center",marginBottom:8}}>
          <div style={{fontFamily:"'DM Mono',monospace",fontSize:34,fontWeight:500,letterSpacing:4,color:timerRunning?C.lime:endTime?"rgba(255,255,255,.55)":"rgba(255,255,255,.18)"}}
            className={timerRunning?"blink":""}>
            {fmtSecs(elapsed)}
          </div>
          {(startTime||endTime)&&(
            <div style={{display:"flex",gap:14,justifyContent:"center",marginTop:2}}>
              {startTime&&<div style={{fontSize:9,color:"rgba(255,255,255,.35)",fontFamily:"'DM Mono',monospace"}}>▶ {fmtDT(startTime)}</div>}
              {endTime&&<div style={{fontSize:9,color:C.pink,fontFamily:"'DM Mono',monospace"}}>■ {fmtDT(endTime)}</div>}
              {endTime&&startTime&&<div style={{fontSize:9,color:C.lime,fontFamily:"'DM Mono',monospace",fontWeight:700}}>{meta.duration||Math.round(elapsed/60)}m</div>}
            </div>
          )}
        </div>

        {/* Start / End */}
        <div style={{display:"flex",gap:8,marginBottom:10}}>
          <button className="btn-start" style={{flex:1,padding:"9px",fontSize:12,letterSpacing:2}} disabled={workoutOn} onClick={handleStart}>▶ START WORKOUT</button>
          <button className="btn-end"   style={{flex:1,padding:"9px",fontSize:12,letterSpacing:2}} disabled={!workoutOn} onClick={handleEnd}>■ END WORKOUT</button>
        </div>

        {/* Name + nav */}
        <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",gap:8}}>
          <div style={{display:"flex",alignItems:"center",gap:8}}>
            <div style={{width:36,height:36,borderRadius:10,flexShrink:0,background:`linear-gradient(135deg,${splitColor},${splitColor}66)`,display:"flex",alignItems:"center",justifyContent:"center",fontSize:18,boxShadow:`0 0 16px ${splitColor}44`,transition:"all 1.2s"}}>⚡</div>
            <div>
              <div style={{fontFamily:"'DM Mono',monospace",fontSize:7,letterSpacing:4,color:"rgba(255,255,255,.3)"}}>IRON LOG</div>
              {editName
                ?<input value={userName} onChange={e=>setUserName(e.target.value.toUpperCase())} onBlur={()=>{setEditName(false);store.sset("il_name",userName)}} onKeyDown={e=>e.key==="Enter"&&setEditName(false)} autoFocus maxLength={14}
                  style={{background:"transparent",border:"none",borderBottom:`1.5px solid ${splitColor}`,color:"#fff",fontSize:15,fontFamily:"'Syne',sans-serif",fontWeight:800,letterSpacing:2,outline:"none",width:140}}/>
                :<div onClick={()=>setEditName(true)} style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:15,letterSpacing:2,cursor:"pointer",display:"flex",alignItems:"center",gap:4,background:`linear-gradient(90deg,#fff 35%,${splitColor})`,WebkitBackgroundClip:"text",WebkitTextFillColor:"transparent"}}>
                  {userName}<span style={{fontSize:10,WebkitTextFillColor:splitColor,opacity:.5}}>✎</span>
                </div>}
            </div>
          </div>
          <div style={{display:"flex",gap:5}}>
            {["LOG","ANALYTICS"].map(v=>(
              <button key={v} className={view===v.toLowerCase()?"btn-lime":"btn-ghost"} style={{padding:"6px 10px",fontSize:10,letterSpacing:1}} onClick={()=>setView(v.toLowerCase())}>{v}</button>
            ))}
          </div>
        </div>
      </div>

      {/* ══ LOG VIEW ══ */}
      {view==="log"&&(
        <div style={{padding:"14px 14px 0",position:"relative",zIndex:10}} className="fadeup">
          {!activeSplit?(
            <div>
              <div style={{marginBottom:16}}>
                <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:26,letterSpacing:2,lineHeight:1,color:"#fff"}}>SELECT <span style={{color:C.lime,textShadow:`0 0 22px ${C.lime}66`}}>SPLIT</span></div>
                <div style={{marginTop:7}}><div className="lglass" style={{fontSize:11,color:"#fff",fontFamily:"'DM Mono',monospace",letterSpacing:2}}>📅 {new Date().toLocaleDateString("en-US",{weekday:"long",month:"long",day:"numeric"}).toUpperCase()}</div></div>
              </div>
              {Object.entries(SPLITS).map(([key,split],i)=>{
                const pct=getProgress(key);const doneToday=!!(logs[today]?.[key]);
                return(
                  <button key={key} className="glass" onClick={()=>handleSplit(key)}
                    style={{width:"100%",marginBottom:10,padding:"15px 17px",cursor:"pointer",display:"flex",alignItems:"center",gap:13,textAlign:"left",border:`1px solid ${doneToday?split.color+"44":"rgba(255,255,255,.08)"}`,animation:`fadeUp .28s ease ${i*.05}s both`}}
                    onMouseEnter={e=>{e.currentTarget.style.borderColor=`${split.color}55`;e.currentTarget.style.transform="translateY(-2px)"}}
                    onMouseLeave={e=>{e.currentTarget.style.borderColor=doneToday?`${split.color}44`:"rgba(255,255,255,.08)";e.currentTarget.style.transform="translateY(-2px)"}}>
                    <div style={{width:50,height:50,borderRadius:14,flexShrink:0,background:`${split.color}18`,border:`1.5px solid ${split.color}33`,display:"flex",alignItems:"center",justifyContent:"center",fontSize:24,boxShadow:`0 0 14px ${split.color}22`}}>{split.emoji}</div>
                    <div style={{flex:1}}>
                      <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:16,letterSpacing:2,color:doneToday?split.color:"#fff"}}>{split.label}</div>
                      <div style={{fontSize:11,color:"rgba(255,255,255,.58)",fontFamily:"'DM Mono',monospace",letterSpacing:1,marginTop:2}}>{split.sub}</div>
                      {pct>0&&<div style={{marginTop:7}}><div className="pbar-track" style={{height:3}}><div className="pbar-fill" style={{width:`${pct}%`,background:split.color}}/></div><div style={{fontSize:9,color:split.color,marginTop:3,fontFamily:"'DM Mono',monospace"}}>{pct}% LOGGED TODAY</div></div>}
                    </div>
                    <div style={{width:28,height:28,borderRadius:8,background:`${split.color}18`,border:`1px solid ${split.color}33`,display:"flex",alignItems:"center",justifyContent:"center",color:split.color,fontSize:15,fontWeight:700}}>›</div>
                  </button>
                );
              })}
            </div>
          ):(
            <div>
              <div style={{display:"flex",alignItems:"center",gap:10,marginBottom:14}}>
                <button className="btn-ghost" style={{padding:"7px 11px",fontSize:11,letterSpacing:1}} onClick={()=>setActiveSplit(null)}>‹ BACK</button>
                <div style={{flex:1}}>
                  <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:19,letterSpacing:3,background:`linear-gradient(90deg,#fff 30%,${splitColor})`,WebkitBackgroundClip:"text",WebkitTextFillColor:"transparent"}}>{SPLITS[activeSplit].emoji} {SPLITS[activeSplit].label}</div>
                  <div style={{marginTop:3}}><div className="lglass" style={{fontSize:9,color:"rgba(255,255,255,.78)",fontFamily:"'DM Mono',monospace",letterSpacing:1}}>{SPLITS[activeSplit].sub}</div></div>
                </div>
                {activeSplit!=="CARDIO"&&(
                  <div style={{textAlign:"center"}}>
                    <div style={{fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:24,color:splitColor,lineHeight:1,textShadow:`0 0 18px ${splitColor}66`}}>{getProgress(activeSplit)}%</div>
                    <div className="pbar-track" style={{width:42,marginTop:3,height:4}}><div className="pbar-fill" style={{width:`${getProgress(activeSplit)}%`,background:splitColor}}/></div>
                  </div>
                )}
              </div>

              {activeSplit==="CARDIO"
                ?<CardioPanel data={logs[today]?.CARDIO?.cardio||{}} onChange={updateCardio} color={splitColor}/>
                :<div>
                  <input value={workoutName} onChange={e=>{setWorkoutName(e.target.value.toUpperCase());store.sset("il_wname",e.target.value.toUpperCase())}}
                    style={{background:"transparent",border:"none",borderBottom:`1px solid ${splitColor}33`,color:"#fff",fontFamily:"'Syne',sans-serif",fontWeight:800,fontSize:13,letterSpacing:2,outline:"none",width:"100%",paddingBottom:5,marginBottom:14,transition:"border-color .2s"}}
                    onFocus={e=>e.target.style.borderBottomColor=splitColor}
                    onBlur={e=>e.target.style.borderBottomColor=`${splitColor}33`}
                    placeholder="NAME OF THE WORKOUT"/>
                  {(exercises[activeSplit]||DEF[activeSplit]||[]).map((ex,i)=>(
                    <ExCard key={ex.id||i} ex={ex} idx={i} color={splitColor}
                      savedSets={logs[today]?.[activeSplit]?.[i]||null}
                      onSets={sets=>updateSets(activeSplit,i,sets)}
                      onEx={nex=>updateExMeta(activeSplit,i,nex)}
                      onDelete={()=>deleteExercise(activeSplit,i)}
                      prev={getPrev(activeSplit,i)}
                      history={savedHistory}/>
                  ))}
                  <button className="btn-ghost" style={{width:"100%",padding:"11px",fontSize:11,letterSpacing:2,marginBottom:10}}
                    onClick={()=>{
                      const n={id:`${activeSplit}_${Date.now()}`,name:"NEW EXERCISE",sets:3,reps:10,unit:"lb"};
                      setExercises(prev=>({...prev,[activeSplit]:[...(prev[activeSplit]||[]),n]}));
                    }}>
                    + ADD EXERCISE
                  </button>
                </div>
              }

              <button className="btn-lime" onClick={handleSave}
                style={{width:"100%",padding:"15px",fontSize:15,letterSpacing:3,background:savedMsg?"linear-gradient(135deg,#00C853,#00E676)":undefined,boxShadow:savedMsg?"0 4px 22px rgba(0,200,83,.42)":undefined,transition:"all .3s"}}>
                {savedMsg?"✓ SESSION SAVED":"SAVE SESSION"}
              </button>
              <div style={{marginTop:6,textAlign:"center",fontFamily:"'DM Mono',monospace",fontSize:9,color:"rgba(255,255,255,.28)",letterSpacing:1}}>
                ANALYTICS UPDATES ONLY AFTER SAVING
              </div>
            </div>
          )}
        </div>
      )}

      {/* ══ ANALYTICS VIEW ══ */}
      {view==="analytics"&&(
        <div style={{position:"relative",zIndex:10}} className="fadeup">
          <Analytics logs={logs} exercises={exercises} savedHistory={savedHistory}/>
        </div>
      )}
    </div>
  );
}
