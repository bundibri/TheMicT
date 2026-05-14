import Purchases from 'react-native-purchases';
import Paywall from '@revenuecat/purchases-ui-react-native';
const showPaywall = async () => {
    const result = await Paywall.presentPaywall();
    if (result === 'PURCHASED') {
        // Success! The user paid.
    }
};

const FONTS = `@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=DM+Mono:ital,wght@0,300;0,400;1,300&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&display=swap');`;

const POEMS = [
  { id:1, title:"Midnight Migration", author:"Sylvie Okafor", category:"Nature",     lines:["The geese do not ask permission","to cross the moon's pale threshold—","they simply rise, and go,","trailing their ragged signatures","across the dark."],                                                                                        reactions:{fire:214,heart:389,star:97},  views:4821,  comments:true,  anonymous:false, avatar:"SO", color:"#c97d4e" },
  { id:2, title:"Salt & Algorithm",   author:"Anonymous",     category:"Technology",  lines:["My grandmother's hands","never once held a device","yet she knew which cloud meant rain,","which silence meant grief.","I call this: intuition.","The engineers call it: lost data."],                                                              reactions:{fire:512,heart:701,star:203}, views:9134,  comments:false, anonymous:true,  avatar:"?",  color:"#7b6fa0" },
  { id:3, title:"After the Diagnosis",author:"Marcus Delaine",category:"Personal",   lines:["The doctor said: benign.","I said: say it again.","He said: benign.","And I sat there learning","how a single word","can be a door swinging open."],                                                                                              reactions:{fire:88,heart:1204,star:445}, views:11203, comments:true,  anonymous:false, avatar:"MD", color:"#4e8c7a" },
  { id:4, title:"Concrete Pastoral",  author:"Yara Ndiaye",   category:"Urban",       lines:["Between the bodega and the laundromat","a single dandelion holds its ground,","gold as ambition,","doomed as everything","that grows without permission."],                                                                                       reactions:{fire:334,heart:567,star:189}, views:6302,  comments:true,  anonymous:false, avatar:"YN", color:"#c9734e" },
];

const LIVE_NOW = [
  { id:1, author:"Sylvie Okafor", avatar:"SO", color:"#c97d4e", title:"Midnight Migration", mode:"video", viewers:84,  poemId:1 },
  { id:2, author:"Anonymous",     avatar:"?",  color:"#7b6fa0", title:"Salt & Algorithm",   mode:"audio", viewers:211, poemId:2 },
];

const UPCOMING = [
  { id:3, author:"Marcus Delaine", avatar:"MD", color:"#4e8c7a", title:"After the Diagnosis", mode:"video", scheduledIn:"in 2 hrs",     poemReady:true,  visibility:"live" },
  { id:4, author:"Yara Ndiaye",    avatar:"YN", color:"#c9734e", title:"Concrete Pastoral",   mode:"audio", scheduledIn:"Tomorrow 8PM", poemReady:true,  visibility:"post" },
  { id:5, author:"Remi Cross",     avatar:"RC", color:"#4e6e8c", title:"Untitled Draft",      mode:"video", scheduledIn:"May 20 7PM",   poemReady:false, visibility:"live" },
];

const EVENTS = [
  { id:1, venue:"The Moth & Lantern",  city:"Brooklyn, NY",    date:"May 16", time:"8:00 PM", theme:"Open Theme",    spots:6,  color:"#c97d4e" },
  { id:2, venue:"Cafe Noir",           city:"New Orleans, LA", date:"May 18", time:"7:30 PM", theme:"Love & Loss",   spots:3,  color:"#7b6fa0" },
  { id:3, venue:"The Ink Well",        city:"Portland, OR",    date:"May 22", time:"9:00 PM", theme:"City Stories",  spots:12, color:"#4e8c7a" },
  { id:4, venue:"Spoken Ground",       city:"Chicago, IL",     date:"May 25", time:"7:00 PM", theme:"Debut Night",   spots:8,  color:"#c9734e" },
  { id:5, venue:"Luna Stage",          city:"Austin, TX",      date:"June 1", time:"8:30 PM", theme:"Memory & Place",spots:5,  color:"#a07b4e" },
  { id:6, venue:"The Loft Collective", city:"Seattle, WA",     date:"June 3", time:"7:00 PM", theme:"Open Theme",    spots:10, color:"#4e6e8c" },
];

const AWARDS = [
  { rank:1, title:"Salt & Algorithm",    author:"Anonymous",      award:"Most Reacted Poem", icon:"⚡", views:9134,  reactions:1416, color:"#D4A853" },
  { rank:2, title:"After the Diagnosis", author:"Marcus Delaine", award:"Most Viewed Poem",  icon:"👁", views:11203, reactions:1737, color:"#C0C0C0" },
  { rank:3, title:"Midnight Migration",  author:"Sylvie Okafor",  award:"Rising Star",       icon:"🌙", views:4821,  reactions:700,  color:"#CD7F32" },
  { rank:4, title:"Concrete Pastoral",   author:"Yara Ndiaye",    award:"Community Choice",  icon:"🌱", views:6302,  reactions:1090, color:"#4e8c7a" },
];

const CATEGORIES = ["All","Nature","Technology","Personal","Urban","Love","Politics","Humor","Experimental"];
const WH = [8,18,30,22,12,36,24,14,40,28,16,44,20,10,32,26,18,42,30,14,22,38,16,28,12,34,20,10];

// ─── AUDIO WAVE ───────────────────────────────────────────────────────────────
function AudioWave({ color="#D4A853", active=true, size="md" }) {
  const bars = size==="sm" ? WH.slice(0,14) : WH;
  const sc   = size==="sm" ? 0.55 : 1;
  return (
    <div style={{display:"flex",alignItems:"center",justifyContent:"center",gap:size==="sm"?2:3,height:size==="sm"?30:54}}>
      {bars.map((v,i)=>(
        <div key={i} style={{width:size==="sm"?2:3,borderRadius:2,background:color,opacity:active?0.8:0.18,
          height:active?v*sc:3,animationName:active?`wv${i}`:"none",
          animationDuration:`${0.5+(i%6)*0.1}s`,animationTimingFunction:"ease-in-out",
          animationDelay:`${(i*0.04).toFixed(2)}s`,animationIterationCount:"infinite",animationDirection:"alternate"}}/>
      ))}
      <style>{bars.map((v,i)=>`@keyframes wv${i}{from{height:${Math.max(2,(v*sc)-6)}px}to{height:${(v*sc)+6}px}}`).join("")}</style>
    </div>
  );
}

function Av({ av, color, size=36 }) {
  return (
    <div style={{width:size,height:size,borderRadius:"50%",background:color,display:"flex",alignItems:"center",
      justifyContent:"center",fontFamily:"'DM Mono',monospace",fontSize:size*0.3,color:"#0d0c0a",flexShrink:0}}>{av}</div>
  );
}

function VideoFeed({ color="#c97d4e", height=200 }) {
  return (
    <div style={{height,background:`radial-gradient(ellipse at 50% 40%,${color}18 0%,#080706 70%)`,
      position:"relative",display:"flex",alignItems:"center",justifyContent:"center",overflow:"hidden"}}>
      <div style={{position:"absolute",inset:0,opacity:0.035,backgroundSize:"160px",
        backgroundImage:"url(\"data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E\")"}}/>
      {[["top:8px;left:8px","top","left"],["top:8px;right:8px","top","right"],["bottom:8px;left:8px","bottom","left"],["bottom:8px;right:8px","bottom","right"]].map(([pos],i)=>(
        <div key={i} style={{position:"absolute",width:16,height:16,borderColor:color+"55",opacity:0.6,
          ...Object.fromEntries(pos.split(";").map(p=>{const[k,...v]=p.split(":");return[k.trim(),v.join(":").trim()];})
          ),borderTop:pos.includes("top:8")?"2px solid":undefined,borderBottom:pos.includes("bottom:8")?"2px solid":undefined,
          borderLeft:pos.includes("left:8")?"2px solid":undefined,borderRight:pos.includes("right:8")?"2px solid":undefined}}/>
      ))}
      <div style={{textAlign:"center"}}>
        <div style={{fontSize:40,marginBottom:6}}>🎥</div>
        <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color,letterSpacing:".1em",opacity:0.65}}>LIVE · VIDEO STREAM</div>
      </div>
    </div>
  );
}

function AudioFeed({ color="#7b6fa0" }) {
  return (
    <div style={{height:120,background:`radial-gradient(ellipse at 50% 80%,${color}20,#080706)`,
      display:"flex",flexDirection:"column",alignItems:"center",justifyContent:"center",gap:8}}>
      <div style={{width:50,height:50,borderRadius:"50%",background:color+"28",border:`1px solid ${color}44`,
        display:"flex",alignItems:"center",justifyContent:"center",fontSize:20}}>🎙</div>
      <AudioWave color={color} active size="sm"/>
      <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color,letterSpacing:".1em",opacity:0.65}}>AUDIO ONLY · VOICE STREAM</div>
    </div>
  );
}

// ─── WATCH SCREEN ─────────────────────────────────────────────────────────────
function WatchScreen({ stream, onClose }) {
  const poem = POEMS.find(p => p.id === stream.poemId);
  const [line, setLine]       = useState(0);
  const [playing, setPlaying] = useState(false);
  const [floaters, setFloaters] = useState([]);
  const timer = useRef(null);

  useEffect(()=>{
    if(playing && poem){
      timer.current = setInterval(()=>{
        setLine(l=>{
          if(l>=poem.lines.length-1){ setPlaying(false); clearInterval(timer.current); return l; }
          return l+1;
        });
      },3000);
      return ()=>clearInterval(timer.current);
    }
  },[playing,poem]);

  const react = e => {
    const id = Date.now()+Math.random();
    setFloaters(f=>[...f,{id,e}]);
    setTimeout(()=>setFloaters(f=>f.filter(x=>x.id!==id)),2500);
  };

  return (
    <div style={{position:"fixed",top:0,left:"50%",transform:"translateX(-50%)",width:"100%",maxWidth:430,
      height:"100dvh",background:"#080706",zIndex:300,display:"flex",flexDirection:"column"}}>
      <style>{`@keyframes floatUp{0%{opacity:1;transform:translateY(0)}100%{opacity:0;transform:translateY(-90px)}}`}</style>

      {/* Top bar */}
      <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",padding:"14px 16px 0",flexShrink:0}}>
        <div style={{display:"flex",alignItems:"center",gap:8}}>
          <div style={{width:7,height:7,borderRadius:"50%",background:"#e05c5c",animation:"pulse 1.5s infinite"}}/>
          <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#e05c5c",letterSpacing:".1em"}}>{stream.viewers} WATCHING</span>
        </div>
        <div style={{display:"flex",gap:6,alignItems:"center"}}>
          <span style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:6,padding:"3px 8px",
            fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".05em"}}>
            {stream.mode==="video"?"📹 LIVE VIDEO":"🎙 AUDIO ONLY"}
          </span>
          <button onClick={onClose} style={{background:"rgba(255,255,255,.06)",border:"none",borderRadius:20,
            color:"#e8e0d0",fontFamily:"'DM Mono',monospace",fontSize:10,padding:"6px 14px",cursor:"pointer"}}>✕</button>
        </div>
      </div>

      {/* Feed */}
      {stream.mode==="video" ? <VideoFeed color={stream.color} height={190}/> : <AudioFeed color={stream.color}/>}

      {/* Caption header */}
      <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",padding:"10px 18px 8px",
        borderBottom:"1px solid #1a1915",flexShrink:0}}>
        <div>
          <div style={{fontFamily:"'Playfair Display',serif",fontSize:16,fontStyle:"italic",color:"#e8e0d0"}}>{poem?.title}</div>
          <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:2,letterSpacing:".05em"}}>
            {stream.author} · caption queue
          </div>
        </div>
        <button onClick={()=>setPlaying(p=>!p)}
          style={{background:playing?"#1a1915":"#D4A853",border:"none",borderRadius:8,
            color:playing?"#D4A853":"#0d0c0a",fontFamily:"'DM Mono',monospace",fontSize:9,
            letterSpacing:".06em",padding:"7px 12px",cursor:"pointer",textTransform:"uppercase"}}>
          {playing?"⏸ Pause":"▶ Sync"}
        </button>
      </div>

      {/* Lines */}
      <div style={{flex:1,overflowY:"auto",padding:"14px 18px"}}>
        {poem?.lines.map((ln,i)=>(
          <div key={i} style={{display:"flex",alignItems:"flex-start",gap:10,marginBottom:14}}>
            <div style={{width:3,borderRadius:2,minHeight:22,flexShrink:0,marginTop:3,transition:"background .3s",
              background: i<line?"#2a2820":i===line?"#D4A853":"#1e1d18"}}/>
            <div style={{fontFamily:"'Cormorant Garamond',serif",fontStyle:"italic",lineHeight:1.55,transition:"all .4s",
              fontSize:i===line?21:16,color:i<line?"#2a2820":i===line?"#e8e0d0":"#3e3c34"}}>
              {ln}
            </div>
          </div>
        ))}
      </div>

      {/* Reactions */}
      <div style={{padding:"10px 16px 20px",borderTop:"1px solid #1a1915",flexShrink:0,position:"relative"}}>
        <div style={{position:"absolute",bottom:70,right:14,display:"flex",flexDirection:"column-reverse",
          alignItems:"flex-end",gap:2,pointerEvents:"none"}}>
          {floaters.map(f=>(
            <div key={f.id} style={{fontSize:22,animation:"floatUp 2.4s ease forwards"}}>{f.e}</div>
          ))}
        </div>
        <div style={{display:"flex",gap:8}}>
          {[["🔥","Fire"],["❤️","Love"],["⭐","Star"],["✨","Wow"]].map(([e,l])=>(
            <button key={l} onClick={()=>react(e)}
              style={{flex:1,background:"#13120e",border:"1px solid #2a2820",borderRadius:12,
                padding:"10px 0",fontSize:18,cursor:"pointer",textAlign:"center"}}>
              {e}
            </button>
          ))}
        </div>
      </div>
    </div>
  );
}

// ─── GO LIVE WIZARD ────────────────────────────────────────────────────────────
function GoLiveWizard({ onClose, onLive }) {
  const [step, setStep]     = useState(1);
  const [mode, setMode]     = useState(null);
  const [vis, setVis]       = useState(null);
  const [poemTitle, setPT]  = useState("");
  const [poemText,  setPX]  = useState("");
  const [submitted, setSub] = useState(false);

  const poemReady = submitted || poemTitle.trim().length > 0;

  const ModeCard = ({ id, icon, title, desc, tags }) => (
    <div onClick={()=>setMode(id)} style={{background:"#1a1915",border:`1px solid ${mode===id?"#D4A853":"#2a2820"}`,
      borderRadius:12,padding:"18px 16px",cursor:"pointer",marginBottom:10,transition:"all .2s"}}>
      <div style={{fontSize:28,marginBottom:8}}>{icon}</div>
      <div style={{fontFamily:"'Playfair Display',serif",fontSize:18,fontStyle:"italic",color:"#e8e0d0"}}>{title}</div>
      <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:5,lineHeight:1.65,letterSpacing:".04em"}}>{desc}</div>
      <div style={{display:"flex",gap:6,marginTop:10,flexWrap:"wrap"}}>
        {tags.map(t=><span key={t} style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:6,padding:"3px 9px",fontFamily:"'DM Mono',monospace",fontSize:9,color:"#6b6456",letterSpacing:".05em"}}>{t}</span>)}
      </div>
    </div>
  );

  const VisCard = ({ id, icon, title, desc }) => (
    <div onClick={()=>setVis(id)} style={{background:"#1a1915",border:`1px solid ${vis===id?"#D4A853":"#2a2820"}`,
      borderRadius:12,padding:16,cursor:"pointer",marginBottom:10,display:"flex",gap:14,alignItems:"flex-start",transition:"all .2s"}}>
      <div style={{fontSize:26,flexShrink:0,marginTop:2}}>{icon}</div>
      <div>
        <div style={{fontFamily:"'Playfair Display',serif",fontSize:17,fontStyle:"italic",color:"#e8e0d0"}}>{title}</div>
        <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:5,lineHeight:1.65,letterSpacing:".04em"}}>{desc}</div>
      </div>
    </div>
  );

  const NextBtn = ({ label, disabled, onClick }) => (
    <button onClick={onClick} disabled={disabled}
      style={{flex:2,background:disabled?"#2a2820":"#D4A853",border:"none",borderRadius:10,
        color:disabled?"#4a4438":"#0d0c0a",fontFamily:"'Playfair Display',serif",fontSize:17,
        fontStyle:"italic",fontWeight:700,padding:12,cursor:disabled?"not-allowed":"pointer"}}>
      {label}
    </button>
  );

  const BackBtn = ({ onClick }) => (
    <button onClick={onClick} style={{flex:1,background:"none",border:"1px solid #2a2820",borderRadius:10,
      color:"#6b6456",fontFamily:"'DM Mono',monospace",fontSize:10,letterSpacing:".06em",
      textTransform:"uppercase",padding:12,cursor:"pointer"}}>← Back</button>
  );

  return (
    <div style={{position:"fixed",top:0,left:"50%",transform:"translateX(-50%)",width:"100%",maxWidth:430,
      height:"100dvh",background:"#0d0c0a",zIndex:300,overflowY:"auto"}}>
      <div style={{padding:"20px 20px 100px"}}>

        <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",marginBottom:24}}>
          <div style={{fontFamily:"'Playfair Display',serif",fontSize:22,fontWeight:900,fontStyle:"italic",color:"#D4A853"}}>
            Verse<span style={{color:"#e8e0d0",fontWeight:400}}>light</span>
          </div>
          <button onClick={onClose} style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:20,
            color:"#6b6456",fontFamily:"'DM Mono',monospace",fontSize:10,padding:"6px 14px",cursor:"pointer"}}>Cancel</button>
        </div>

        {/* Step bar */}
        <div style={{display:"flex",gap:6,marginBottom:24}}>
          {[1,2,3,4].map(s=>(
            <div key={s} style={{flex:1,height:2,borderRadius:2,transition:"background .3s",background:step>=s?"#D4A853":"#2a2820"}}/>
          ))}
        </div>

        {/* ── STEP 1: Mode ── */}
        {step===1 && (
          <>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".1em",textTransform:"uppercase",marginBottom:6}}>Step 1 of 4</div>
            <div style={{fontFamily:"'Playfair Display',serif",fontSize:24,fontStyle:"italic",color:"#e8e0d0",marginBottom:6}}>Choose Your Format</div>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".04em",marginBottom:22,lineHeight:1.7}}>How would you like to perform tonight?</div>
            <ModeCard id="video" icon="📹" title="Live Video" desc="Stream from your phone camera. Your face, your presence — the full performance visible to your audience in real time." tags={["camera on","face visible","full performance"]}/>
            <ModeCard id="audio" icon="🎙" title="Audio Only" desc="Your voice is the instrument. Stream audio without showing your face — perfect for privacy or keeping the focus purely on the words." tags={["voice only","no camera","stay private"]}/>
            <button onClick={()=>setStep(2)} disabled={!mode}
              style={{width:"100%",background:mode?"#D4A853":"#2a2820",border:"none",borderRadius:10,
                color:mode?"#0d0c0a":"#4a4438",fontFamily:"'Playfair Display',serif",fontSize:18,
                fontStyle:"italic",fontWeight:700,padding:15,cursor:mode?"pointer":"not-allowed",marginTop:4}}>
              Continue →
            </button>
          </>
        )}

        {/* ── STEP 2: Visibility ── */}
        {step===2 && (
          <>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".1em",textTransform:"uppercase",marginBottom:6}}>Step 2 of 4</div>
            <div style={{fontFamily:"'Playfair Display',serif",fontSize:24,fontStyle:"italic",color:"#e8e0d0",marginBottom:6}}>Who Can Watch?</div>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".04em",marginBottom:22,lineHeight:1.7}}>Choose when your performance is seen.</div>
            <VisCard id="live" icon="🌐" title="Live — Open to All" desc="Viewers join in real time as you perform. Reactions flow live. Your recording saves and posts automatically when you finish."/>
            <VisCard id="post" icon="🕰" title="Record & Post Later" desc="No live viewers. Perform privately — we record and upload your performance after you finish, so you can post on your own terms."/>
            <div style={{display:"flex",gap:8,marginTop:8}}>
              <BackBtn onClick={()=>setStep(1)}/>
              <NextBtn label="Continue →" disabled={!vis} onClick={()=>setStep(3)}/>
            </div>
          </>
        )}

        {/* ── STEP 3: Poem ── */}
        {step===3 && (
          <>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".1em",textTransform:"uppercase",marginBottom:6}}>Step 3 of 4</div>
            <div style={{fontFamily:"'Playfair Display',serif",fontSize:24,fontStyle:"italic",color:"#e8e0d0",marginBottom:6}}>Poem Submission</div>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".04em",marginBottom:20,lineHeight:1.75}}>
              Poems must be submitted at least <span style={{color:"#D4A853"}}>24 hours before</span> your live — so we can format your caption queue. If your poem is already on file, you're ready.
            </div>

            {/* Status */}
            <div style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:12,padding:16,marginBottom:14}}>
              <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",marginBottom:10}}>Poem Status</div>
              {poemReady ? (
                <div style={{display:"flex",alignItems:"center",gap:10}}>
                  <div style={{width:32,height:32,borderRadius:"50%",background:"#1a2e1a",border:"1px solid #4e8c7a",display:"flex",alignItems:"center",justifyContent:"center",fontSize:14,flexShrink:0}}>✓</div>
                  <div>
                    <div style={{fontFamily:"'Cormorant Garamond',serif",fontSize:16,color:"#4e8c7a"}}>Poem ready for captioning</div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:2}}>
                      {submitted?"Submitted just now — queued for review":"Submitted 26h ago · captions prepared"}
                    </div>
                  </div>
                </div>
              ) : (
                <div style={{display:"flex",alignItems:"center",gap:10}}>
                  <div style={{width:32,height:32,borderRadius:"50%",background:"#2e1a1a",border:"1px solid #7a4e4e",display:"flex",alignItems:"center",justifyContent:"center",fontSize:14,flexShrink:0}}>⚠</div>
                  <div>
                    <div style={{fontFamily:"'Cormorant Garamond',serif",fontSize:16,color:"#c97d4e"}}>No poem on file yet</div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:2}}>Submit below — your live will unlock 24hrs after submission</div>
                  </div>
                </div>
              )}
            </div>

            {!poemReady && (
              <div style={{marginBottom:14}}>
                <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",marginBottom:6}}>Submit Your Poem</div>
                <input placeholder="Poem title" value={poemTitle} onChange={e=>setPT(e.target.value)}
                  style={{width:"100%",background:"#13120e",border:"1px solid #2a2820",borderRadius:9,
                    color:"#e8e0d0",fontFamily:"'Cormorant Garamond',serif",fontSize:16,padding:"11px 14px",
                    outline:"none",marginBottom:8}}/>
                <textarea placeholder={"Enter each line of your poem here...\n\nThese become your live caption queue."} 
                  value={poemText} onChange={e=>setPX(e.target.value)} rows={5}
                  style={{width:"100%",background:"#13120e",border:"1px solid #2a2820",borderRadius:9,
                    color:"#c8bfa8",fontFamily:"'Cormorant Garamond',serif",fontStyle:"italic",fontSize:15,
                    padding:14,outline:"none",resize:"none",lineHeight:1.8,marginBottom:8}}/>
                <button onClick={()=>setSub(true)} disabled={!poemTitle||!poemText}
                  style={{width:"100%",background:poemTitle&&poemText?"#1a2e1a":"#13120e",
                    border:`1px solid ${poemTitle&&poemText?"#4e8c7a":"#2a2820"}`,borderRadius:9,
                    color:poemTitle&&poemText?"#4e8c7a":"#3a3526",fontFamily:"'DM Mono',monospace",
                    fontSize:10,letterSpacing:".06em",textTransform:"uppercase",padding:12,cursor:"pointer"}}>
                  Submit Poem — Live unlocks in 24 hrs
                </button>
              </div>
            )}

            <div style={{display:"flex",gap:8,marginTop:6}}>
              <BackBtn onClick={()=>setStep(2)}/>
              <NextBtn label="Continue →" disabled={!poemReady} onClick={()=>setStep(4)}/>
            </div>
          </>
        )}

        {/* ── STEP 4: Confirm ── */}
        {step===4 && (
          <>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".1em",textTransform:"uppercase",marginBottom:6}}>Step 4 of 4</div>
            <div style={{fontFamily:"'Playfair Display',serif",fontSize:24,fontStyle:"italic",color:"#e8e0d0",marginBottom:6}}>Ready to Perform?</div>
            <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".04em",marginBottom:20,lineHeight:1.7}}>Here's your setup. Once you go live, the stage is yours.</div>

            <div style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:12,padding:16,marginBottom:14}}>
              {[
                ["Format",       mode==="video"?"📹 Live Video":"🎙 Audio Only"],
                ["Audience",     vis==="live"?"🌐 Live — open to viewers":"🕰 Private — uploads after"],
                ["Caption queue","✓ Poem prepared & formatted"],
                ["Recording",    "✓ Always saved to your profile"],
              ].map(([k,v],i,arr)=>(
                <div key={k} style={{display:"flex",justifyContent:"space-between",alignItems:"center",
                  marginBottom:i<arr.length-1?12:0,paddingBottom:i<arr.length-1?12:0,
                  borderBottom:i<arr.length-1?"1px solid #1e1d18":"none"}}>
                  <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase"}}>{k}</div>
                  <div style={{fontFamily:"'Cormorant Garamond',serif",fontSize:15,color:"#e8e0d0"}}>{v}</div>
                </div>
              ))}
            </div>

            <div style={{background:"#0d0c0a",border:"1px solid #2a2215",borderRadius:10,padding:"12px 14px",marginBottom:16}}>
              <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#D4A853",letterSpacing:".06em",marginBottom:4}}>💡 TIP</div>
              <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",lineHeight:1.75}}>
                Your caption queue will highlight line by line as you perform. Viewers see the poem text synced alongside your {mode==="video"?"video":"audio"} stream.
              </div>
            </div>

            <div style={{display:"flex",gap:8}}>
              <BackBtn onClick={()=>setStep(3)}/>
              <button onClick={onLive} style={{flex:2,background:"#e05c5c",border:"none",borderRadius:10,color:"#fff",
                fontFamily:"'Playfair Display',serif",fontSize:18,fontStyle:"italic",fontWeight:700,
                padding:12,cursor:"pointer",letterSpacing:".01em"}}>
                🔴 Go Live
              </button>
            </div>
          </>
        )}
      </div>
    </div>
  );
}

// ─── MAIN APP ─────────────────────────────────────────────────────────────────
const CSS = `
  ${FONTS}
  *{box-sizing:border-box;margin:0;padding:0;}
  body{background:#0d0c0a;}
  .vl{font-family:'Cormorant Garamond',Georgia,serif;background:#0d0c0a;color:#e8e0d0;min-height:100vh;max-width:430px;margin:0 auto;position:relative;}
  .hdr{padding:20px 22px 0;display:flex;justify-content:space-between;align-items:center;}
  .logo{font-family:'Playfair Display',serif;font-size:22px;font-weight:900;font-style:italic;letter-spacing:-.5px;color:#D4A853;}
  .logo span{color:#e8e0d0;font-weight:400;}
  .topnav{display:flex;gap:2px;padding:14px 12px 0;overflow-x:auto;scrollbar-width:none;}
  .topnav::-webkit-scrollbar{display:none;}
  .tnb{flex-shrink:0;background:none;border:1px solid #2a2820;border-radius:20px;color:#6b6456;font-family:'DM Mono',monospace;font-size:10px;letter-spacing:.05em;padding:6px 14px;cursor:pointer;transition:all .2s;text-transform:uppercase;}
  .tnb.on{background:#D4A853;border-color:#D4A853;color:#0d0c0a;}
  .content{padding:16px 0 100px;}
  .st{font-family:'Playfair Display',serif;font-size:28px;font-weight:700;font-style:italic;padding:10px 22px 4px;color:#e8e0d0;}
  .ss{font-family:'DM Mono',monospace;font-size:10px;color:#5a5448;padding:0 22px 16px;letter-spacing:.08em;text-transform:uppercase;}
  @keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.8)}}
  .ltabs{display:flex;margin:0 16px 16px;background:#13120e;border:1px solid #2a2820;border-radius:10px;padding:4px;}
  .ltab{flex:1;background:none;border:none;border-radius:7px;color:#5a5448;font-family:'DM Mono',monospace;font-size:10px;letter-spacing:.06em;text-transform:uppercase;padding:9px;cursor:pointer;transition:all .2s;}
  .ltab.on{background:#D4A853;color:#0d0c0a;}
  .scard{margin:0 16px 10px;background:#13120e;border:1px solid #2a2820;border-radius:14px;overflow:hidden;cursor:pointer;transition:border-color .2s;}
  .scard:hover{border-color:#3a3526;}
  .sinfo{display:flex;align-items:center;gap:10px;padding:10px 14px 12px;}
  .sname{font-family:'Playfair Display',serif;font-size:15px;color:#e8e0d0;}
  .ldot{width:7px;height:7px;border-radius:50%;background:#e05c5c;animation:pulse 1.5s infinite;}
  .upcard{margin:0 16px 8px;background:#13120e;border:1px solid #2a2820;border-radius:10px;padding:12px 14px;display:flex;align-items:center;gap:12px;}
  .cats{display:flex;gap:6px;padding:0 22px 14px;overflow-x:auto;scrollbar-width:none;}
  .cats::-webkit-scrollbar{display:none;}
  .chip{flex-shrink:0;background:none;border:1px solid #2a2820;border-radius:20px;color:#6b6456;font-family:'DM Mono',monospace;font-size:10px;padding:5px 12px;cursor:pointer;transition:all .2s;text-transform:uppercase;letter-spacing:.05em;}
  .chip.on{background:#2a2215;border-color:#D4A853;color:#D4A853;}
  .pcard2{margin:0 16px 10px;background:#13120e;border:1px solid #2a2820;border-radius:14px;overflow:hidden;cursor:pointer;transition:border-color .2s;}
  .pcard2:hover{border-color:#3a3526;}
  .pheader{display:flex;align-items:center;gap:10px;padding:14px 16px 10px;}
  .pmeta{flex:1;min-width:0;}
  .pauthor{font-family:'Playfair Display',serif;font-size:14px;color:#e8e0d0;}
  .pcat{font-family:'DM Mono',monospace;font-size:9px;color:#5a5448;letter-spacing:.08em;text-transform:uppercase;}
  .ptitle2{font-family:'Playfair Display',serif;font-size:19px;font-style:italic;font-weight:700;padding:0 16px 8px;color:#e8e0d0;}
  .pprev{font-family:'Cormorant Garamond',serif;font-size:15px;font-style:italic;color:#8a8070;padding:0 16px 12px;line-height:1.6;}
  .pfull{font-family:'Cormorant Garamond',serif;font-size:16px;font-style:italic;color:#c8bfa8;padding:14px 16px 12px;border-top:1px solid #2a2820;line-height:1.8;}
  .pfooter{display:flex;align-items:center;gap:6px;padding:10px 16px 14px;border-top:1px solid #1e1d18;}
  .rb{background:#1a1915;border:1px solid #2a2820;border-radius:20px;padding:5px 10px;font-size:12px;cursor:pointer;display:flex;align-items:center;gap:5px;transition:all .15s;}
  .rb:hover{border-color:#D4A853;transform:scale(1.05);}
  .rc{font-family:'DM Mono',monospace;font-size:9px;color:#8a8070;}
  .sform{padding:0 20px;display:flex;flex-direction:column;gap:14px;}
  .sinput{width:100%;background:#13120e;border:1px solid #2a2820;border-radius:10px;color:#e8e0d0;font-family:'Cormorant Garamond',serif;font-size:17px;padding:12px 14px;outline:none;transition:border-color .2s;}
  .sinput:focus{border-color:#D4A853;}
  .sinput::placeholder{color:#3a3526;}
  .starea{width:100%;background:#13120e;border:1px solid #2a2820;border-radius:10px;color:#c8bfa8;font-family:'Cormorant Garamond',serif;font-style:italic;font-size:17px;padding:14px;outline:none;resize:none;line-height:1.8;min-height:160px;transition:border-color .2s;}
  .starea:focus{border-color:#D4A853;}
  .starea::placeholder{color:#3a3526;font-style:italic;}
  .strow{display:flex;align-items:center;justify-content:space-between;background:#13120e;border:1px solid #2a2820;border-radius:10px;padding:13px 16px;}
  .stlabel{font-family:'Cormorant Garamond',serif;font-size:16px;color:#e8e0d0;}
  .stdesc{font-family:'DM Mono',monospace;font-size:9px;color:#5a5448;margin-top:2px;}
  .tog{width:42px;height:24px;border-radius:12px;background:#2a2820;position:relative;cursor:pointer;transition:background .25s;border:none;flex-shrink:0;}
  .tog.on{background:#D4A853;}
  .tog::after{content:'';position:absolute;top:3px;left:3px;width:18px;height:18px;border-radius:50%;background:#e8e0d0;transition:transform .25s;}
  .tog.on::after{transform:translateX(18px);}
  .ssbtn{width:100%;background:#D4A853;border:none;border-radius:12px;color:#0d0c0a;font-family:'Playfair Display',serif;font-size:18px;font-style:italic;font-weight:700;padding:16px;cursor:pointer;}
  .ssbtn:hover{opacity:.9;}
  .sel{background:#1a1915;border:1px solid #2a2820;border-radius:10px;color:#e8e0d0;font-family:'DM Mono',monospace;font-size:11px;padding:10px 14px;width:100%;outline:none;appearance:none;cursor:pointer;}
  .evcard{margin:0 16px 10px;background:#13120e;border:1px solid #2a2820;border-radius:14px;padding:16px;display:flex;gap:14px;}
  .evdate{text-align:center;flex-shrink:0;width:48px;}
  .evmonth{font-family:'DM Mono',monospace;font-size:9px;color:#5a5448;text-transform:uppercase;letter-spacing:.08em;}
  .evday{font-family:'Playfair Display',serif;font-size:28px;font-weight:900;line-height:1;color:#e8e0d0;}
  .evvenue{font-family:'Playfair Display',serif;font-size:17px;font-style:italic;color:#e8e0d0;}
  .evcity{font-family:'DM Mono',monospace;font-size:10px;color:#5a5448;margin:3px 0 8px;letter-spacing:.04em;}
  .evtags{display:flex;gap:6px;flex-wrap:wrap;}
  .evtag{border-radius:6px;padding:3px 8px;font-family:'DM Mono',monospace;font-size:9px;letter-spacing:.05em;}
  .rsvp{background:none;border:1px solid #D4A853;border-radius:8px;color:#D4A853;font-family:'DM Mono',monospace;font-size:9px;padding:6px 12px;cursor:pointer;transition:all .2s;letter-spacing:.06em;text-transform:uppercase;margin-top:10px;}
  .rsvp:hover{background:#D4A853;color:#0d0c0a;}
  .awcard{margin:0 16px 10px;background:#13120e;border:1px solid #2a2820;border-radius:14px;padding:16px;position:relative;overflow:hidden;}
  .awrank{font-family:'Playfair Display',serif;font-size:56px;font-weight:900;position:absolute;right:12px;top:50%;transform:translateY(-50%);opacity:.07;color:#e8e0d0;line-height:1;}
  .awtype{font-family:'DM Mono',monospace;font-size:9px;letter-spacing:.1em;text-transform:uppercase;margin-bottom:4px;}
  .awtitle{font-family:'Playfair Display',serif;font-size:20px;font-style:italic;font-weight:700;color:#e8e0d0;}
  .awauthor{font-family:'DM Mono',monospace;font-size:10px;color:#5a5448;margin:4px 0 10px;}
  .awstats{display:flex;gap:16px;}
  .awstat{font-family:'DM Mono',monospace;font-size:10px;color:#6b6456;}
  .awstat b{color:#e8e0d0;font-weight:400;}
  .bnav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:430px;background:rgba(13,12,10,.96);border-top:1px solid #2a2820;display:flex;padding:10px 8px 18px;gap:4px;backdrop-filter:blur(12px);}
  .bb{flex:1;background:none;border:none;display:flex;flex-direction:column;align-items:center;gap:4px;cursor:pointer;padding:6px 4px;border-radius:10px;transition:background .2s;}
  .bb.on{background:#1a1915;}
  .bicon{font-size:18px;line-height:1;}
  .blabel{font-family:'DM Mono',monospace;font-size:8px;letter-spacing:.06em;text-transform:uppercase;color:#4a4438;transition:color .2s;}
  .bb.on .blabel{color:#D4A853;}
`;

export default function App(import { Platform } from 'react-native';
import { useEffect } from 'react';
import Purchases, { LOG_LEVEL } from 'react-native-purchases';

export default function App() {
  useEffect(() => {
    Purchases.setLogLevel(LOG_LEVEL.VERBOSE);

    // Platform-specific API keys
    const iosApiKey = 'test_BhgdgeltGCErOAWNSMAjLJUHCDq';
    const androidApiKey = 'test_BhgdgeltGCErOAWNSMAjLJUHCDq';

    if (Platform.OS === 'ios') {
       Purchases.configure({apiKey: iosApiKey});
    } else if (Platform.OS === 'android') {
       Purchases.configure({apiKey: androidApiKey});
    }
  }, []);
}
) {
  const [tab, setTab]             = useState("live");
  const [liveTab, setLiveTab]     = useState("watch");
  const [watching, setWatching]   = useState(null);
  const [goingLive, setGoingLive] = useState(false);
  const [selectedCat, setCat]     = useState("All");
  const [reactions, setReactions] = useState({});
  const [expanded, setExpanded]   = useState(null);
  const [form, setForm]           = useState({ title:"", text:"", category:"Personal", comments:true, anonymous:false });
  const [submitted, setSubmitted] = useState(false);

  const toggleR = (id,t) => setReactions(r=>({...r,[`${id}-${t}`]:!r[`${id}-${t}`]}));
  const getC    = (p,t)  => p.reactions[t]+(reactions[`${p.id}-${t}`]?1:0);
  const filtered = selectedCat==="All" ? POEMS : POEMS.filter(p=>p.category===selectedCat);

  return (
    <>
      <style>{CSS}</style>
      {watching   && <WatchScreen   stream={watching} onClose={()=>setWatching(null)}/>}
      {goingLive  && <GoLiveWizard  onClose={()=>setGoingLive(false)} onLive={()=>{setGoingLive(false);alert("🔴 You're live! (Camera/mic access would begin here in the real app.)");}}/>}

      <div className="vl">
        <div className="hdr">
          <div className="logo">Verse<span>light</span></div>
          <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase"}}>
            {{"live":"The Stage","discover":"Browse Poems","submit":"Your Stage","events":"Find a Mic","awards":"Hall of Fame"}[tab]}
          </div>
        </div>

        <div className="topnav">
          {[["live","🎙 Live"],["discover","📜 Discover"],["submit","✍ Submit"],["events","📍 Events"],["awards","🏆 Awards"]].map(([id,l])=>(
            <button key={id} className={`tnb${tab===id?" on":""}`} onClick={()=>setTab(id)}>{l}</button>
          ))}
        </div>

        <div className="content">

          {/* ══ LIVE ══ */}
          {tab==="live" && (
            <>
              <div className="st">The Stage</div>
              <div className="ss">Live performances · Caption queue · On-demand</div>

              <div className="ltabs">
                <button className={`ltab${liveTab==="watch"?" on":""}`} onClick={()=>setLiveTab("watch")}>Watch</button>
                <button className={`ltab${liveTab==="perform"?" on":""}`} onClick={()=>setLiveTab("perform")}>Perform</button>
              </div>

              {liveTab==="watch" && (
                <>
                  <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",padding:"0 16px 8px",display:"flex",alignItems:"center",gap:8}}>
                    <div className="ldot"/><span>Live Now</span>
                  </div>

                  {LIVE_NOW.map(s=>(
                    <div key={s.id} className="scard" onClick={()=>setWatching(s)}>
                      {s.mode==="video"
                        ? <VideoFeed color={s.color} height={100}/>
                        : <div style={{height:80,background:`radial-gradient(ellipse at 50% 80%,${s.color}20,#080706)`,display:"flex",alignItems:"center",justifyContent:"center"}}>
                            <AudioWave color={s.color} active size="sm"/>
                          </div>
                      }
                      <div className="sinfo">
                        <Av av={s.avatar} color={s.color} size={38}/>
                        <div style={{flex:1,minWidth:0}}>
                          <div className="sname">{s.author}</div>
                          <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:2,fontStyle:"italic",color:"#7a7060"}}>{s.title}</div>
                        </div>
                        <div style={{display:"flex",flexDirection:"column",alignItems:"flex-end",gap:4,flexShrink:0}}>
                          <span style={{background:s.mode==="video"?"#2e1a1a":"#1a1a2e",border:`1px solid ${s.mode==="video"?"#7a4e4e":"#4e4e7a"}`,borderRadius:6,padding:"2px 7px",fontFamily:"'DM Mono',monospace",fontSize:9,color:s.mode==="video"?"#c97d4e":"#7b6fa0",letterSpacing:".05em"}}>
                            {s.mode==="video"?"📹 VIDEO":"🎙 AUDIO"}
                          </span>
                          <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448"}}>{s.viewers} watching</span>
                        </div>
                      </div>
                      <div style={{padding:"8px 14px 12px",borderTop:"1px solid #1e1d18",display:"flex",justifyContent:"space-between",alignItems:"center"}}>
                        <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#4e8c7a",letterSpacing:".06em"}}>✓ Caption queue ready</span>
                        <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#D4A853",letterSpacing:".06em"}}>Tap to watch →</span>
                      </div>
                    </div>
                  ))}

                  <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",padding:"10px 16px 8px"}}>Upcoming Performances</div>
                  {UPCOMING.map(u=>(
                    <div key={u.id} className="upcard">
                      <Av av={u.avatar} color={u.color} size={38}/>
                      <div style={{flex:1,minWidth:0}}>
                        <div style={{fontFamily:"'Playfair Display',serif",fontSize:14,fontStyle:"italic",color:"#e8e0d0",whiteSpace:"nowrap",overflow:"hidden",textOverflow:"ellipsis"}}>{u.title}</div>
                        <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:2}}>{u.author} · {u.scheduledIn}</div>
                      </div>
                      <div style={{display:"flex",flexDirection:"column",alignItems:"flex-end",gap:4,flexShrink:0}}>
                        <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:u.mode==="video"?"#c97d4e":"#7b6fa0"}}>{u.mode==="video"?"📹":"🎙"}</span>
                        <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:u.poemReady?"#4e8c7a":"#7a4e4e"}}>{u.poemReady?"✓ poem ready":"⚠ poem pending"}</span>
                        <span style={{fontFamily:"'DM Mono',monospace",fontSize:8,color:"#4a4438",letterSpacing:".04em"}}>{u.visibility==="live"?"🌐 live":"🕰 posts after"}</span>
                      </div>
                    </div>
                  ))}
                </>
              )}

              {liveTab==="perform" && (
                <div style={{padding:"0 16px"}}>
                  <div style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:14,padding:20,marginBottom:12}}>
                    <div style={{fontFamily:"'Playfair Display',serif",fontSize:20,fontStyle:"italic",color:"#e8e0d0",marginBottom:8}}>Your stage awaits.</div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",lineHeight:1.8,letterSpacing:".04em",marginBottom:18}}>
                      Perform live from your phone — with or without your face on screen. Your poem displays line by line alongside your stream so viewers can follow along in real time.
                    </div>
                    <div style={{display:"flex",gap:6,flexWrap:"wrap",marginBottom:18}}>
                      {[["📹","Live video"],["🎙","Audio only"],["📜","Caption queue"],["🌐","Live or post-after"],["💾","Always recorded"]].map(([i,l])=>(
                        <span key={l} style={{background:"#1a1915",border:"1px solid #2a2820",borderRadius:20,padding:"4px 10px",fontFamily:"'DM Mono',monospace",fontSize:9,color:"#6b6456",display:"flex",alignItems:"center",gap:5}}>
                          <span>{i}</span><span style={{letterSpacing:".04em"}}>{l}</span>
                        </span>
                      ))}
                    </div>
                    <button onClick={()=>setGoingLive(true)}
                      style={{width:"100%",background:"#e05c5c",border:"none",borderRadius:12,color:"#fff",
                        fontFamily:"'Playfair Display',serif",fontSize:20,fontStyle:"italic",fontWeight:700,
                        padding:16,cursor:"pointer"}}>
                      🔴 Set Up Your Live
                    </button>
                  </div>

                  <div style={{background:"#13100a",border:"1px solid #2a2215",borderRadius:12,padding:"14px 16px",marginBottom:12}}>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#D4A853",letterSpacing:".06em",marginBottom:6}}>⏱ THE 24-HOUR RULE</div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",lineHeight:1.75}}>
                      Your poem must be submitted at least <span style={{color:"#D4A853"}}>24 hours before</span> going live. This lets us prepare your caption queue so viewers can read along line by line as you perform.
                    </div>
                  </div>

                  {[{icon:"📹",label:"Live Video",sub:"Stream from your camera. Viewers see your face and can react in real time.",color:"#c97d4e"},
                    {icon:"🎙",label:"Audio Only",sub:"Recite by voice. No camera required — your presence lives in the words alone.",color:"#7b6fa0"}].map(m=>(
                    <div key={m.label} style={{background:"#13120e",border:"1px solid #2a2820",borderRadius:12,padding:"14px 16px",marginBottom:8,display:"flex",gap:14,alignItems:"flex-start"}}>
                      <div style={{width:38,height:38,borderRadius:"50%",background:m.color+"18",display:"flex",alignItems:"center",justifyContent:"center",fontSize:20,flexShrink:0}}>{m.icon}</div>
                      <div>
                        <div style={{fontFamily:"'Playfair Display',serif",fontSize:16,fontStyle:"italic",color:"#e8e0d0"}}>{m.label}</div>
                        <div style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#5a5448",marginTop:4,lineHeight:1.65,letterSpacing:".04em"}}>{m.sub}</div>
                      </div>
                    </div>
                  ))}
                </div>
              )}
            </>
          )}

          {/* ══ DISCOVER ══ */}
          {tab==="discover" && (
            <>
              <div className="st">Discover</div>
              <div className="ss">Poems from the community</div>
              <div className="cats">
                {CATEGORIES.map(c=><button key={c} className={`chip${selectedCat===c?" on":""}`} onClick={()=>setCat(c)}>{c}</button>)}
              </div>
              {filtered.map(poem=>(
                <div key={poem.id} className="pcard2" onClick={()=>setExpanded(expanded===poem.id?null:poem.id)}>
                  <div className="pheader">
                    <Av av={poem.avatar} color={poem.color} size={36}/>
                    <div className="pmeta">
                      <div className="pauthor">{poem.anonymous?"Anonymous":poem.author}</div>
                      <div className="pcat">{poem.category}</div>
                    </div>
                    {poem.anonymous && <span style={{background:"#1f1e18",border:"1px solid #3a3526",borderRadius:6,padding:"3px 8px",fontFamily:"'DM Mono',monospace",fontSize:9,color:"#7b6fa0",letterSpacing:".06em"}}>anon</span>}
                  </div>
                  <div className="ptitle2">{poem.title}</div>
                  {expanded===poem.id
                    ? <div className="pfull">{poem.lines.map((l,i)=><div key={i}>{l}</div>)}</div>
                    : <div className="pprev">{poem.lines[0]}</div>}
                  <div className="pfooter">
                    {[["fire","🔥"],["heart","❤️"],["star","⭐"]].map(([t,e])=>(
                      <button key={t} className="rb" style={reactions[`${poem.id}-${t}`]?{borderColor:"#D4A853"}:{}}
                        onClick={ev=>{ev.stopPropagation();toggleR(poem.id,t);}}>
                        <span>{e}</span><span className="rc">{getC(poem,t).toLocaleString()}</span>
                      </button>
                    ))}
                    {!poem.comments && <span style={{fontFamily:"'DM Mono',monospace",fontSize:9,color:"#3a3526",marginLeft:4}}>💬 off</span>}
                    <span style={{marginLeft:"auto",fontFamily:"'DM Mono',monospace",fontSize:9,color:"#4a4438"}}>👁 {poem.views.toLocaleString()}</span>
                  </div>
                </div>
              ))}
            </>
          )}

          {/* ══ SUBMIT ══ */}
          {tab==="submit" && (
            <>
              <div className="st">Your Stage</div>
              <div className="ss">Share your work with the world</div>
              {submitted ? (
                <div style={{textAlign:"center",padding:"40px 20px"}}>
                  <div style={{fontSize:48,marginBottom:16}}>🕯️</div>
                  <div style={{fontFamily:"'Playfair Display',serif",fontSize:26,fontStyle:"italic",color:"#D4A853",marginBottom:8}}>Your poem is live.</div>
                  <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",marginBottom:24}}>The stage is yours.</div>
                  <button className="ssbtn" onClick={()=>{setSubmitted(false);setForm({title:"",text:"",category:"Personal",comments:true,anonymous:false});}}>Submit Another</button>
                </div>
              ) : (
                <div className="sform">
                  <div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",marginBottom:6}}>Poem Title</div>
                    <input className="sinput" placeholder="What shall we call it?" value={form.title} onChange={e=>setForm(f=>({...f,title:e.target.value}))}/>
                  </div>
                  <div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",marginBottom:6}}>Your Poem</div>
                    <textarea className="starea" placeholder={"Begin here...\n\nEach line, a breath."} value={form.text} onChange={e=>setForm(f=>({...f,text:e.target.value}))}/>
                  </div>
                  <div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",marginBottom:6}}>Category</div>
                    <select className="sel" value={form.category} onChange={e=>setForm(f=>({...f,category:e.target.value}))}>
                      {CATEGORIES.filter(c=>c!=="All").map(c=><option key={c}>{c}</option>)}
                    </select>
                  </div>
                  <div>
                    <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#5a5448",letterSpacing:".08em",textTransform:"uppercase",marginBottom:8}}>Preferences</div>
                    {[{key:"comments",label:"Allow Comments",desc:"Readers can leave feedback"},{key:"anonymous",label:"Stay Anonymous",desc:"Name hidden. Reactions still reach you privately."}].map(({key,label,desc})=>(
                      <div key={key} className="strow" style={{marginBottom:8}}>
                        <div><div className="stlabel">{label}</div><div className="stdesc">{desc}</div></div>
                        <button className={`tog${form[key]?" on":""}`} onClick={()=>setForm(f=>({...f,[key]:!f[key]}))}/>
                      </div>
                    ))}
                  </div>
                  <button className="ssbtn" disabled={!form.title||!form.text} style={{opacity:(!form.title||!form.text)?0.4:1}} onClick={()=>setSubmitted(true)}>
                    Publish to the Stage →
                  </button>
                </div>
              )}
            </>
          )}

          {/* ══ EVENTS ══ */}
          {tab==="events" && (
            <>
              <div className="st">Open Mics</div>
              <div className="ss">Local events · Nationwide stages</div>
              {EVENTS.map(ev=>{
                const[month,day]=ev.date.split(" ");
                return(
                  <div key={ev.id} className="evcard">
                    <div className="evdate"><div className="evmonth">{month}</div><div className="evday">{day}</div></div>
                    <div style={{flex:1,minWidth:0}}>
                      <div className="evvenue">{ev.venue}</div>
                      <div className="evcity">📍 {ev.city}</div>
                      <div className="evtags">
                        <span className="evtag" style={{background:ev.color+"22",color:ev.color}}>{ev.theme}</span>
                        <span className="evtag" style={{background:"#1a1915",color:"#5a5448"}}>⏰ {ev.time}</span>
                      </div>
                      <div style={{fontFamily:"'DM Mono',monospace",fontSize:10,color:"#D4A853",marginTop:10}}>{ev.spots} spots remaining</div>
                      <button className="rsvp">RSVP to Perform</button>
                    </div>
                  </div>
                );
              })}
              <div style={{height:1,background:"#1e1d18",margin:"4px 16px 14px"}}/>
              <div style={{padding:"0 16px"}}><button className="rsvp" style={{width:"100%",textAlign:"center",padding:14}}>+ List Your Venue's Open Mic Night</button></div>
            </>
          )}

          {/* ══ AWARDS ══ */}
          {tab==="awards" && (
            <>
              <div className="st">Hall of Fame</div>
              <div className="ss">Annual recognition · 2025 season</div>
              <div style={{fontFamily:"'DM Mono',monospace",fontSize:11,color:"#5a5448",letterSpacing:".12em",textAlign:"center",paddingBottom:16,textTransform:"uppercase"}}>— 2025 Verselight Awards —</div>
              {AWARDS.map(a=>(
                <div key={a.rank} className="awcard">
                  <div className="awrank">{a.rank}</div>
                  <div style={{fontSize:20,marginBottom:6}}>{a.icon}</div>
                  <div className="awtype" style={{color:a.color}}>{a.award}</div>
                  <div className="awtitle">{a.title}</div>
                  <div className="awauthor">by {a.author}</div>
                  <div className="awstats">
                    <div className="awstat">👁 <b>{a.views.toLocaleString()}</b> views</div>
                    <div className="awstat">⚡ <b>{a.reactions.toLocaleString()}</b> reactions</div>
                  </div>
                </div>
              ))}
            </>
          )}

        </div>

        <div className="bnav">
          {[["live","🎙","Stage"],["discover","📜","Discover"],["submit","✍","Submit"],["events","📍","Events"],["awards","🏆","Awards"]].map(([id,icon,label])=>(
            <button key={id} className={`bb${tab===id?" on":""}`} onClick={()=>setTab(id)}>
              <span className="bicon">{icon}</span>
              <span className="blabel">{label}</span>
            </button>
          ))}
        </div>
      </div>
    </>
  );
}

