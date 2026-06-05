import { useState, useEffect, useCallback } from "react";

const SB_URL = 'https://cxunxveutyuhspjeswgq.supabase.co';
const SB_KEY = 'sb_publishable_lqOPzImzgI0B_pbnTLmyFA_5USemX2c';
const H = { 'Content-Type':'application/json', 'apikey': SB_KEY, 'Authorization': `Bearer ${SB_KEY}`, 'Prefer': 'return=representation' };

const sb = {
  get: async (table, query='') => { const r = await fetch(`${SB_URL}/rest/v1/${table}?${query}`, {headers:H}); return r.ok ? r.json() : []; },
  post: async (table, body) => { const r = await fetch(`${SB_URL}/rest/v1/${table}`, {method:'POST', headers:H, body:JSON.stringify(body)}); return r.ok ? r.json() : null; },
  patch: async (table, id, body) => { const r = await fetch(`${SB_URL}/rest/v1/${table}?id=eq.${id}`, {method:'PATCH', headers:{...H,'Prefer':'return=minimal'}, body:JSON.stringify(body)}); return r.ok; },
  del: async (table, id) => { const r = await fetch(`${SB_URL}/rest/v1/${table}?id=eq.${id}`, {method:'DELETE', headers:H}); return r.ok; },
};

const HOSPITALS = ["Samsung Medical Center","Asan Medical Center","Severance Hospital (Yonsei)","Seoul National University Hospital","Korea University Anam Hospital","Gangnam Severance Hospital","Seoul St. Mary's Hospital","Bundang Seoul National University Hospital","CHA Bundang Medical Center","Ajou University Medical Center","Pusan National University Hospital","Wooridul Spine Hospital","Nune Eye Hospital","Megahealth Dental Clinic","JCI Korea International Clinic"];
const DEPARTMENTS = ["Cardiology","Cardiothoracic Surgery","Neurology","Neurosurgery","Orthopedics & Joint Replacement","Spine Surgery","Oncology / Cancer Treatment","Radiation Oncology","Hematology","Pediatrics","Pediatric Surgery","General Surgery","Laparoscopic & Robotic Surgery","Dermatology & Aesthetics","Plastic & Reconstructive Surgery","ENT","Cochlear Implant","Ophthalmology / LASIK","Dental & Maxillofacial","Fertility / IVF","Obstetrics & Gynecology","Urology & Kidney Transplant","Nephrology","Gastroenterology & Liver","Liver Transplant","Endocrinology","Rheumatology","Pulmonology","Psychiatry","Physical Therapy & Rehabilitation","Sports Medicine","Stem Cell Therapy","Health Checkup","Traditional Korean Medicine"];
const STATUSES = ["Inquiry","Documents Preparing","Visa Applied","Visa Approved","Flight Booked","Arrived in Korea","In Treatment","Treatment Complete","Returned to Mongolia","Follow-up","Completed","Cancelled"];
const STATUS_COLORS = {"Inquiry":"#f59e0b","Documents Preparing":"#f97316","Visa Applied":"#a78bfa","Visa Approved":"#3b82f6","Flight Booked":"#06b6d4","Arrived in Korea":"#8b5cf6","In Treatment":"#ec4899","Treatment Complete":"#38bdf8","Returned to Mongolia":"#64748b","Follow-up":"#f97316","Completed":"#10b981","Cancelled":"#ef4444"};
const VISA_STATUSES = ["Not Applied","Applied","Approved","Denied","Not Required"];
const TRANSFER_OPTIONS = ["Not Required","Incheon Airport Pickup","Incheon Airport Sendoff","Both Pickup & Sendoff","Gimpo Airport Pickup","Gimpo Airport Sendoff"];
const AIRLINES = ["Korean Air (KE)","Asiana Airlines (OZ)","Air Busan (BX)","Jin Air (LJ)","MIAT Mongolian Airlines (OM)","Other"];
const INSURANCE = ["No Insurance","Mongol Daatgal","MIG Insurance","Nomin Insurance","Khan Insurance","AIG Mongolia","Korean Travel Insurance","Other"];
const COUNTRIES = ["Mongolia","China","Russia","Kazakhstan","Kyrgyzstan","Uzbekistan","Japan","South Korea","India","Other"];
const TABS = ["Dashboard","Inquiries","New Patient","Patients","Appointments","Follow-ups"];
const ICONS = {Dashboard:"◈",Inquiries:"🌐","New Patient":"+",Patients:"♟",Appointments:"⊡","Follow-ups":"✉"};

const uid = () => Math.random().toString(36).slice(2,9);
const today = () => new Date().toISOString().split("T")[0];
const fmtDate = d => d ? new Date(d+"T00:00").toLocaleDateString("en-US",{month:"short",day:"numeric",year:"numeric"}) : "—";
const fmtDT = ts => new Date(ts).toLocaleString("en-US",{month:"short",day:"numeric",hour:"2-digit",minute:"2-digit"});

export default function App() {
  const [tab, setTab] = useState("Dashboard");
  const [patients, setPatients] = useState([]);
  const [appointments, setAppointments] = useState([]);
  const [notes, setNotes] = useState([]);
  const [inquiries, setInquiries] = useState([]);
  const [loading, setLoading] = useState(true);
  const [toast, setToast] = useState(null);
  const [search, setSearch] = useState("");
  const [filterStatus, setFilterStatus] = useState("All");
  const [filterHospital, setFilterHospital] = useState("All");
  const [selectedPatient, setSelectedPatient] = useState(null);
  const [detailTab, setDetailTab] = useState("Info");
  const [noteText, setNoteText] = useState("");
  const [notePatientId, setNotePatientId] = useState("");
  const [saving, setSaving] = useState(false);

  const emptyP = {name:"",age:"",gender:"Male",nationality:"Mongolia",phone:"",email:"",passport_no:"",passport_expiry:"",visa_status:"Not Applied",visa_expiry:"",insurance_provider:"No Insurance",insurance_policy_no:"",arrival_date:"",departure_date:"",airline:"",flight_arrival:"",flight_departure:"",hotel_name:"",hotel_address:"",hotel_checkin:"",hotel_checkout:"",airport_transfer:"Not Required",transfer_notes:"",hospital:HOSPITALS[0],hospital_city:"Seoul",department:DEPARTMENTS[0],doctor:"",consult_date:"",consult_time:"09:00",treatment_notes:"",estimated_cost:"",status:"Inquiry"};
  const [pForm, setPForm] = useState(emptyP);

  const showToast = (msg, type="success") => { setToast({msg,type}); setTimeout(()=>setToast(null),3000); };

  const loadAll = useCallback(async () => {
    setLoading(true);
    const [p, a, n, inq] = await Promise.all([
      sb.get('patients','order=created_at.desc'),
      sb.get('appointments','order=created_at.desc'),
      sb.get('notes','order=created_at.desc'),
      sb.get('inquiries','order=created_at.desc'),
    ]);
    setPatients(p||[]); setAppointments(a||[]); setNotes(n||[]); setInquiries(inq||[]);
    setLoading(false);
  }, []);

  useEffect(() => { loadAll(); }, [loadAll]);

  const addPatient = async () => {
    if (!pForm.name || !pForm.phone) return showToast("Нэр болон утас заавал!", "error");
    setSaving(true);
    const res = await sb.post('patients', pForm);
    if (res && res[0]) {
      if (pForm.consult_date) {
        await sb.post('appointments', {
          patient_id: res[0].id,
          hospital: pForm.hospital,
          department: pForm.department,
          doctor: pForm.doctor,
          appt_date: pForm.consult_date,
          appt_time: pForm.consult_time,
          notes: pForm.treatment_notes,
          status: 'Pending'
        });
      }
      await loadAll();
      setPForm(emptyP);
      showToast(`${pForm.name} амжилттай бүртгэгдлээ!`);
      setTab("Patients");
    } else showToast("Алдаа гарлаа. Дахин оролдоно уу.", "error");
    setSaving(false);
  };

  const updatePatientStatus = async (id, status) => {
    await sb.patch('patients', id, {status});
    setPatients(prev => prev.map(p => p.id===id ? {...p,status} : p));
    if (selectedPatient?.id===id) setSelectedPatient(prev => ({...prev,status}));
    showToast(`→ ${status}`);
  };

  const deletePatient = async id => {
    if (!confirm("Өвчтөн болон бүх мэдээллийг устгах уу?")) return;
    await sb.del('patients', id);
    await loadAll();
    if (selectedPatient?.id===id) setSelectedPatient(null);
    showToast("Устгагдлаа.");
  };

  const addNote = async () => {
    if (!noteText.trim() || !notePatientId) return showToast("Өвчтөн сонгоод тэмдэглэл бичнэ үү.", "error");
    await sb.post('notes', {patient_id: notePatientId, text: noteText.trim()});
    await loadAll();
    setNoteText(""); showToast("Тэмдэглэл хадгалагдлаа.");
  };

  const updateInquiryStatus = async (id, status) => {
    await sb.patch('inquiries', id, {status});
    setInquiries(prev => prev.map(i => i.id===id ? {...i,status} : i));
    showToast(`→ ${status}`);
  };

  if (loading) return <div style={{display:"flex",alignItems:"center",justifyContent:"center",height:"100vh",background:"#080e1a",color:"#38bdf8",fontFamily:"Inter,sans-serif",flexDirection:"column",gap:12}}><div style={{fontSize:32}}>🏥</div><div>Supabase-аас татаж байна...</div></div>;

  const S = {
    app:{fontFamily:"'Inter',system-ui,sans-serif",background:"#080e1a",minHeight:"100vh",color:"#e2e8f0",display:"flex"},
    sb:{width:215,background:"#0d1526",borderRight:"1px solid #1e2d45",display:"flex",flexDirection:"column",padding:"0 0 16px",flexShrink:0,position:"sticky",top:0,height:"100vh"},
    lb:{padding:"16px 14px 12px",borderBottom:"1px solid #1e2d45"},
    nb:a=>({display:"flex",alignItems:"center",gap:9,padding:"10px 16px",cursor:"pointer",border:"none",background:a?"linear-gradient(90deg,#cd2e3a22,#00347822)":"transparent",color:a?"#fff":"#64748b",fontSize:12,fontWeight:a?700:400,textAlign:"left",width:"100%",borderLeft:a?"3px solid #38bdf8":"3px solid transparent"}),
    main:{flex:1,overflow:"auto",padding:"22px 26px"},
    card:{background:"#0d1526",border:"1px solid #1e2d45",borderRadius:12,padding:18},
    sc:c=>({background:"#0d1526",border:`1px solid ${c}33`,borderRadius:12,padding:"14px 18px",borderLeft:`4px solid ${c}`}),
    g4:{display:"grid",gridTemplateColumns:"repeat(4,1fr)",gap:13,marginBottom:20},
    g2:{display:"grid",gridTemplateColumns:"1fr 1fr",gap:14},
    g3:{display:"grid",gridTemplateColumns:"1fr 1fr 1fr",gap:13},
    lbl:{display:"block",fontSize:10,fontWeight:700,color:"#475569",marginBottom:5,textTransform:"uppercase",letterSpacing:"0.07em"},
    inp:{width:"100%",background:"#080e1a",border:"1px solid #1e2d45",borderRadius:7,padding:"8px 11px",color:"#e2e8f0",fontSize:12,outline:"none",boxSizing:"border-box"},
    sel:{width:"100%",background:"#080e1a",border:"1px solid #1e2d45",borderRadius:7,padding:"8px 11px",color:"#e2e8f0",fontSize:12,outline:"none",boxSizing:"border-box"},
    btn:{background:"linear-gradient(135deg,#cd2e3a,#003478)",color:"#fff",border:"none",borderRadius:8,padding:"10px 22px",fontSize:12,fontWeight:700,cursor:"pointer"},
    bsm:(c="#1d4ed8")=>({background:c,color:"#fff",border:"none",borderRadius:5,padding:"3px 8px",fontSize:10,fontWeight:700,cursor:"pointer",whiteSpace:"nowrap"}),
    badge:st=>({background:(STATUS_COLORS[st]||"#475569")+"22",color:STATUS_COLORS[st]||"#94a3b8",border:`1px solid ${STATUS_COLORS[st]||"#475569"}44`,borderRadius:20,padding:"2px 9px",fontSize:10,fontWeight:700,display:"inline-block"}),
    sh:{fontSize:10,fontWeight:700,color:"#38bdf8",textTransform:"uppercase",letterSpacing:"0.1em",marginBottom:9,marginTop:4,paddingBottom:5,borderBottom:"1px solid #1e2d45"},
    fg:{marginBottom:12},
    tbl:{width:"100%",borderCollapse:"collapse"},
    th:{textAlign:"left",fontSize:10,color:"#475569",fontWeight:700,padding:"7px 11px",textTransform:"uppercase",borderBottom:"1px solid #1e2d45"},
    td:{padding:"10px 11px",borderBottom:"1px solid #0a1120",fontSize:12},
    toast:t=>({position:"fixed",bottom:20,right:20,background:t==="error"?"#dc2626":"#059669",color:"#fff",padding:"10px 18px",borderRadius:9,fontSize:12,fontWeight:700,zIndex:9999}),
    dtb:a=>({background:a?"#1e2d45":"transparent",color:a?"#38bdf8":"#64748b",border:"none",borderRadius:6,padding:"6px 12px",fontSize:11,fontWeight:a?700:400,cursor:"pointer"}),
    fr:{display:"flex",gap:8,marginBottom:13,flexWrap:"wrap",alignItems:"center"},
    ir:{display:"flex",justifyContent:"space-between",padding:"6px 0",borderBottom:"1px solid #1e2d45",fontSize:12},
  };

  const IR = ({label,val}) => val ? <div style={S.ir}><span style={{color:"#475569",fontSize:11}}>{label}</span><span style={{color:"#e2e8f0",fontWeight:500,textAlign:"right",maxWidth:"62%"}}>{val}</span></div> : null;

  const matchSearch = p => {
    if (!search) return true;
    const q = search.toLowerCase();
    return p.name?.toLowerCase().includes(q) || (p.hospital||"").toLowerCase().includes(q) || (p.department||"").toLowerCase().includes(q) || (p.phone||"").includes(q) || (p.doctor||"").toLowerCase().includes(q);
  };

  const filteredPatients = patients.filter(p => matchSearch(p) && (filterStatus==="All"||(p.status||"Inquiry")===filterStatus) && (filterHospital==="All"||p.hospital===filterHospital));

  const todayAppts = appointments.filter(a => a.appt_date===today());
  const inKorea = patients.filter(p=>["Arrived in Korea","In Treatment","Treatment Complete"].includes(p.status)).length;
  const activeCount = patients.filter(p=>["Visa Approved","Flight Booked","Arrived in Korea","In Treatment"].includes(p.status)).length;
  const newInquiries = inquiries.filter(i=>i.status==='New').length;

  // DASHBOARD
  const renderDashboard = () => (
    <>
      <div style={S.g4}>
        {[{l:"Нийт өвчтөн",v:patients.length,c:"#3b82f6"},{l:"Солонгост байгаа",v:inKorea,c:"#ec4899"},{l:"Идэвхтэй кейс",v:activeCount,c:"#8b5cf6"},{l:"Шинэ хүсэлт",v:newInquiries,c:"#f59e0b"}].map(({l,v,c})=>(
          <div key={l} style={S.sc(c)}><div style={{fontSize:26,fontWeight:800,color:"#fff"}}>{v}</div><div style={{fontSize:11,color:"#64748b",marginTop:3}}>{l}</div></div>
        ))}
      </div>
      <div style={S.g2}>
        <div style={S.card}>
          <div style={S.sh}>Өвчтөний явц</div>
          {STATUSES.map(st=>{const cnt=patients.filter(p=>(p.status||"Inquiry")===st).length; return cnt>0?(
            <div key={st} style={{display:"flex",justifyContent:"space-between",alignItems:"center",padding:"7px 0",borderBottom:"1px solid #1e2d45"}}>
              <span style={S.badge(st)}>{st}</span><span style={{fontWeight:700,fontSize:13}}>{cnt}</span>
            </div>
          ):null;})}
          {!patients.length&&<div style={{color:"#475569",fontSize:12}}>Өвчтөн байхгүй байна.</div>}
        </div>
        <div style={S.card}>
          <div style={S.sh}>Өнөөдрийн цаг захиалга</div>
          {todayAppts.map(a=>{const pt=patients.find(p=>p.id===a.patient_id); return(<div key={a.id} style={{padding:"8px 0",borderBottom:"1px solid #1e2d45"}}><div style={{fontWeight:600,fontSize:12}}>{pt?.name||"—"}</div><div style={{fontSize:10,color:"#475569"}}>{a.appt_time} · {a.department} · {a.hospital}</div></div>);})}
          {!todayAppts.length&&<div style={{color:"#475569",fontSize:12}}>Өнөөдөр цаг захиалга байхгүй.</div>}
          <div style={{...S.sh,marginTop:16}}>Өнөөдрийн трансфер 🚐</div>
          {patients.filter(p=>p.arrival_date===today()&&p.airport_transfer!=="Not Required").map(p=><div key={p.id} style={{fontSize:12,padding:"6px 0",borderBottom:"1px solid #1e2d45"}}>🛬 <strong>{p.name}</strong> <span style={{color:"#475569",fontSize:10}}>· {p.airline} {p.flight_arrival}</span></div>)}
          {patients.filter(p=>p.departure_date===today()&&p.airport_transfer!=="Not Required").map(p=><div key={p.id} style={{fontSize:12,padding:"6px 0",borderBottom:"1px solid #1e2d45"}}>🛫 <strong>{p.name}</strong> <span style={{color:"#475569",fontSize:10}}>· {p.flight_departure}</span></div>)}
          {!patients.filter(p=>p.arrival_date===today()||p.departure_date===today()).length&&<div style={{color:"#475569",fontSize:12}}>Өнөөдөр трансфер байхгүй.</div>}
        </div>
      </div>
    </>
  );

  // INQUIRIES
  const renderInquiries = () => {
    const iColors={New:"#f59e0b",Contacted:"#3b82f6",Converted:"#10b981",Closed:"#ef4444"};
    const iBadge=st=>({background:(iColors[st]||"#475569")+"22",color:iColors[st]||"#94a3b8",border:`1px solid ${iColors[st]||"#475569"}44`,borderRadius:20,padding:"2px 9px",fontSize:10,fontWeight:700,display:"inline-block"});
    return(
      <>
        <div style={S.fr}>
          <button style={{...S.btn,padding:"8px 16px",fontSize:11}} onClick={loadAll}>🔄 Шинэчлэх</button>
          <span style={{color:"#475569",fontSize:11}}>{inquiries.length} хүсэлт</span>
          <span style={{background:"#f59e0b22",color:"#f59e0b",border:"1px solid #f59e0b44",borderRadius:20,padding:"2px 10px",fontSize:10,fontWeight:700}}>{newInquiries} шинэ</span>
        </div>
        {!inquiries.length?(
          <div style={{...S.card,textAlign:"center",padding:40}}>
            <div style={{fontSize:32,marginBottom:12}}>🌐</div>
            <div style={{fontWeight:700,marginBottom:8}}>Хүсэлт байхгүй байна</div>
            <div style={{fontSize:12,color:"#475569"}}>Вэбсайтын форм бөглөгдөх бүрт энд харагдана</div>
          </div>
        ):(
          <div style={{...S.card,padding:0,overflow:"hidden"}}>
            <table style={S.tbl}>
              <thead><tr style={{background:"#0a1120"}}>
                {["Огноо","Нэр","Утас","И-мэйл","Чиглэл","Мэдэгдэл","Хэл","Статус",""].map(h=><th key={h} style={S.th}>{h}</th>)}
              </tr></thead>
              <tbody>{inquiries.map(inq=>(
                <tr key={inq.id} style={{background:"#0d1526"}}>
                  <td style={S.td}><div style={{fontSize:10,color:"#475569"}}>{new Date(inq.created_at).toLocaleDateString()}</div></td>
                  <td style={S.td}><div style={{fontWeight:700}}>{inq.name}</div></td>
                  <td style={S.td}>{inq.phone}</td>
                  <td style={S.td}><div style={{fontSize:11,color:"#475569"}}>{inq.email||"—"}</div></td>
                  <td style={S.td}><div style={{fontSize:11}}>{inq.department||"—"}</div></td>
                  <td style={S.td}><div style={{fontSize:11,color:"#94a3b8",maxWidth:150,overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>{inq.message||"—"}</div></td>
                  <td style={S.td}><span style={{fontSize:10,fontWeight:700,color:"#38bdf8"}}>{inq.language||"—"}</span></td>
                  <td style={S.td}><span style={iBadge(inq.status||"New")}>{inq.status||"New"}</span></td>
                  <td style={S.td}>
                    <div style={{display:"flex",gap:4,flexWrap:"wrap"}}>
                      {["Contacted","Converted","Closed"].filter(st=>st!==(inq.status||"New")).map(st=>(
                        <button key={st} style={S.bsm(st==="Converted"?"#059669":st==="Contacted"?"#1d4ed8":"#dc2626")} onClick={()=>updateInquiryStatus(inq.id,st)}>{st}</button>
                      ))}
                      <button style={S.bsm("#7c3aed")} onClick={()=>{
                        setPForm({...emptyP,name:inq.name,phone:inq.phone,email:inq.email||"",department:inq.department||DEPARTMENTS[0]});
                        setTab("New Patient"); showToast("Мэдээлэл шилжүүлэгдлээ!");
                      }}>→ Бүртгэх</button>
                    </div>
                  </td>
                </tr>
              ))}</tbody>
            </table>
          </div>
        )}
      </>
    );
  };

  // NEW PATIENT
  const renderNewPatient = () => (
    <div style={{maxWidth:720}}>
      <div style={S.card}>
        <div style={S.sh}>Хувийн мэдээлэл</div>
        <div style={S.g3}>
          <div style={S.fg}><label style={S.lbl}>Нэр *</label><input style={S.inp} value={pForm.name} onChange={e=>setPForm({...pForm,name:e.target.value})} placeholder="Овог нэр"/></div>
          <div style={S.fg}><label style={S.lbl}>Нас</label><input style={S.inp} type="number" value={pForm.age} onChange={e=>setPForm({...pForm,age:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Хүйс</label><select style={S.sel} value={pForm.gender} onChange={e=>setPForm({...pForm,gender:e.target.value})}><option>Male</option><option>Female</option><option>Other</option></select></div>
        </div>
        <div style={S.g3}>
          <div style={S.fg}><label style={S.lbl}>Харьяалал</label><select style={S.sel} value={pForm.nationality} onChange={e=>setPForm({...pForm,nationality:e.target.value})}>{COUNTRIES.map(c=><option key={c}>{c}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Утас *</label><input style={S.inp} value={pForm.phone} onChange={e=>setPForm({...pForm,phone:e.target.value})} placeholder="+976 ..."/></div>
          <div style={S.fg}><label style={S.lbl}>И-мэйл</label><input style={S.inp} value={pForm.email} onChange={e=>setPForm({...pForm,email:e.target.value})}/></div>
        </div>
        <div style={S.sh}>Паспорт & Виз</div>
        <div style={S.g3}>
          <div style={S.fg}><label style={S.lbl}>Паспортын №</label><input style={S.inp} value={pForm.passport_no} onChange={e=>setPForm({...pForm,passport_no:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Паспорт дуусах</label><input style={S.inp} type="date" value={pForm.passport_expiry} onChange={e=>setPForm({...pForm,passport_expiry:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Визний статус</label><select style={S.sel} value={pForm.visa_status} onChange={e=>setPForm({...pForm,visa_status:e.target.value})}>{VISA_STATUSES.map(v=><option key={v}>{v}</option>)}</select></div>
        </div>
        <div style={S.sh}>Даатгал</div>
        <div style={S.g2}>
          <div style={S.fg}><label style={S.lbl}>Даатгалын компани</label><select style={S.sel} value={pForm.insurance_provider} onChange={e=>setPForm({...pForm,insurance_provider:e.target.value})}>{INSURANCE.map(i=><option key={i}>{i}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Полисын №</label><input style={S.inp} value={pForm.insurance_policy_no} onChange={e=>setPForm({...pForm,insurance_policy_no:e.target.value})}/></div>
        </div>
        <div style={S.sh}>Нислэг</div>
        <div style={S.g3}>
          <div style={S.fg}><label style={S.lbl}>Авиа компани</label><select style={S.sel} value={pForm.airline} onChange={e=>setPForm({...pForm,airline:e.target.value})}>{AIRLINES.map(a=><option key={a}>{a}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Ирэх огноо</label><input style={S.inp} type="date" value={pForm.arrival_date} onChange={e=>setPForm({...pForm,arrival_date:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Буцах огноо</label><input style={S.inp} type="date" value={pForm.departure_date} onChange={e=>setPForm({...pForm,departure_date:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Ирэх нислэгийн №</label><input style={S.inp} value={pForm.flight_arrival} onChange={e=>setPForm({...pForm,flight_arrival:e.target.value})} placeholder="KE876"/></div>
          <div style={S.fg}><label style={S.lbl}>Буцах нислэгийн №</label><input style={S.inp} value={pForm.flight_departure} onChange={e=>setPForm({...pForm,flight_departure:e.target.value})} placeholder="KE877"/></div>
        </div>
        <div style={S.sh}>Нисэх буудлын трансфер</div>
        <div style={S.g2}>
          <div style={S.fg}><label style={S.lbl}>Трансфер</label><select style={S.sel} value={pForm.airport_transfer} onChange={e=>setPForm({...pForm,airport_transfer:e.target.value})}>{TRANSFER_OPTIONS.map(t=><option key={t}>{t}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Тэмдэглэл</label><input style={S.inp} value={pForm.transfer_notes} onChange={e=>setPForm({...pForm,transfer_notes:e.target.value})} placeholder="Жолооч, машины мэдээлэл..."/></div>
        </div>
        <div style={S.sh}>Байр (Солонгост)</div>
        <div style={S.g2}>
          <div style={S.fg}><label style={S.lbl}>Зочид буудал</label><input style={S.inp} value={pForm.hotel_name} onChange={e=>setPForm({...pForm,hotel_name:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Хаяг</label><input style={S.inp} value={pForm.hotel_address} onChange={e=>setPForm({...pForm,hotel_address:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Нэвтрэх</label><input style={S.inp} type="date" value={pForm.hotel_checkin} onChange={e=>setPForm({...pForm,hotel_checkin:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Гарах</label><input style={S.inp} type="date" value={pForm.hotel_checkout} onChange={e=>setPForm({...pForm,hotel_checkout:e.target.value})}/></div>
        </div>
        <div style={S.sh}>Солонгосын эмнэлэг</div>
        <div style={S.g3}>
          <div style={S.fg}><label style={S.lbl}>Эмнэлэг *</label><select style={S.sel} value={pForm.hospital} onChange={e=>setPForm({...pForm,hospital:e.target.value})}>{HOSPITALS.map(h=><option key={h}>{h}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Тасаг *</label><select style={S.sel} value={pForm.department} onChange={e=>setPForm({...pForm,department:e.target.value})}>{DEPARTMENTS.map(d=><option key={d}>{d}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Эмчийн нэр</label><input style={S.inp} value={pForm.doctor} onChange={e=>setPForm({...pForm,doctor:e.target.value})} placeholder="Солонгос эмчийн нэр"/></div>
        </div>
        <div style={S.g3}>
          <div style={S.fg}><label style={S.lbl}>Цаг захиалгын огноо</label><input style={S.inp} type="date" value={pForm.consult_date} onChange={e=>setPForm({...pForm,consult_date:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Цаг</label><input style={S.inp} type="time" value={pForm.consult_time} onChange={e=>setPForm({...pForm,consult_time:e.target.value})}/></div>
          <div style={S.fg}><label style={S.lbl}>Зардлын тооцоо (USD)</label><input style={S.inp} value={pForm.estimated_cost} onChange={e=>setPForm({...pForm,estimated_cost:e.target.value})} placeholder="$3,500"/></div>
        </div>
        <div style={S.fg}><label style={S.lbl}>Оношилгоо / Эмчилгээний тэмдэглэл</label><textarea style={{...S.inp,height:75,resize:"vertical"}} value={pForm.treatment_notes} onChange={e=>setPForm({...pForm,treatment_notes:e.target.value})} placeholder="Оношилгоо, хүссэн эмчилгээ..."/></div>
        <div style={S.fg}><label style={S.lbl}>Явцын статус</label><select style={S.sel} value={pForm.status} onChange={e=>setPForm({...pForm,status:e.target.value})}>{STATUSES.map(s=><option key={s}>{s}</option>)}</select></div>
        <button style={{...S.btn,opacity:saving?0.6:1}} onClick={addPatient} disabled={saving}>{saving?"Хадгалж байна...":"✓ Өвчтөн бүртгэх"}</button>
      </div>
    </div>
  );

  // PATIENT DETAIL
  const renderDetail = p => {
    const pNotes = notes.filter(n=>n.patient_id===p.id).sort((a,b)=>b.created_at>a.created_at?1:-1);
    const pAppts = appointments.filter(a=>a.patient_id===p.id);
    return(
      <div style={{...S.card,marginTop:14}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",marginBottom:12}}>
          <div>
            <div style={{fontSize:15,fontWeight:800,color:"#fff"}}>{p.name}</div>
            <div style={{fontSize:11,color:"#475569"}}>🇲🇳 {p.nationality} → 🇰🇷 {p.hospital} · {p.department}</div>
          </div>
          <div style={{display:"flex",gap:7,alignItems:"center",flexWrap:"wrap"}}>
            <select style={{...S.sel,width:180}} value={p.status||"Inquiry"} onChange={e=>updatePatientStatus(p.id,e.target.value)}>{STATUSES.map(st=><option key={st}>{st}</option>)}</select>
            <button style={S.bsm("#dc2626")} onClick={()=>deletePatient(p.id)}>Устгах</button>
            <button style={S.bsm("#334155")} onClick={()=>setSelectedPatient(null)}>✕</button>
          </div>
        </div>
        <div style={{display:"flex",gap:6,marginBottom:14}}>
          {["Info","Аялал","Эмнэлэг","Тэмдэглэл"].map(dt=><button key={dt} style={S.dtb(detailTab===dt)} onClick={()=>setDetailTab(dt)}>{dt}</button>)}
        </div>
        {detailTab==="Info"&&<div style={S.g2}><div><div style={S.sh}>Холбоо</div><IR label="Утас" val={p.phone}/><IR label="И-мэйл" val={p.email}/><div style={S.sh}>Паспорт & Виз</div><IR label="Паспортын №" val={p.passport_no}/><IR label="Паспорт дуусах" val={fmtDate(p.passport_expiry)}/><IR label="Визний статус" val={p.visa_status}/></div><div><div style={S.sh}>Даатгал</div><IR label="Компани" val={p.insurance_provider}/><IR label="Полис №" val={p.insurance_policy_no}/><div style={S.sh}>Байр</div><IR label="Зочид буудал" val={p.hotel_name}/><IR label="Хаяг" val={p.hotel_address}/><IR label="Нэвтрэх" val={fmtDate(p.hotel_checkin)}/><IR label="Гарах" val={fmtDate(p.hotel_checkout)}/></div></div>}
        {detailTab==="Аялал"&&<div style={S.g2}><div><div style={S.sh}>Нислэг</div><IR label="Авиа компани" val={p.airline}/><IR label="Ирэх огноо" val={fmtDate(p.arrival_date)}/><IR label="Ирэх нислэг" val={p.flight_arrival}/><IR label="Буцах огноо" val={fmtDate(p.departure_date)}/><IR label="Буцах нислэг" val={p.flight_departure}/></div><div><div style={S.sh}>Трансфер</div><IR label="Төрөл" val={p.airport_transfer}/><IR label="Тэмдэглэл" val={p.transfer_notes}/></div></div>}
        {detailTab==="Эмнэлэг"&&<div><div style={S.sh}>Эмнэлгийн мэдээлэл</div><IR label="Эмнэлэг" val={p.hospital}/><IR label="Тасаг" val={p.department}/><IR label="Эмч" val={p.doctor}/><IR label="Зардал" val={p.estimated_cost}/><IR label="Тэмдэглэл" val={p.treatment_notes}/><div style={{...S.sh,marginTop:14}}>Цаг захиалга</div>{pAppts.length?pAppts.map(a=><div key={a.id} style={{display:"flex",justifyContent:"space-between",padding:"7px 0",borderBottom:"1px solid #1e2d45",fontSize:12}}><div><strong>{fmtDate(a.appt_date)}</strong> {a.appt_time} · {a.department}</div><span style={S.badge(a.status)}>{a.status}</span></div>):<div style={{color:"#475569",fontSize:12}}>Цаг захиалга байхгүй.</div>}</div>}
        {detailTab==="Тэмдэглэл"&&<div><div style={S.sh}>Тэмдэглэлүүд</div><div style={{display:"flex",gap:8,marginBottom:12}}><textarea style={{...S.inp,flex:1,height:55,resize:"none"}} placeholder="Тэмдэглэл бичих..." value={notePatientId===p.id?noteText:""} onChange={e=>{setNoteText(e.target.value);setNotePatientId(p.id);}}/><button style={{...S.btn,padding:"0 14px",alignSelf:"stretch"}} onClick={addNote}>Нэмэх</button></div>{pNotes.length?pNotes.map(n=><div key={n.id} style={{background:"#080e1a",borderRadius:8,padding:"9px 12px",marginBottom:7}}><div style={{fontSize:12,color:"#e2e8f0",lineHeight:1.5}}>{n.text}</div><div style={{fontSize:10,color:"#334155",marginTop:4}}>{fmtDT(n.created_at)}</div></div>):<div style={{color:"#475569",fontSize:12}}>Тэмдэглэл байхгүй.</div>}</div>}
      </div>
    );
  };

  // PATIENTS
  const renderPatients = () => (
    <>
      <div style={S.fr}>
        <input style={{...S.inp,width:230}} placeholder="🔍 Нэр, эмнэлэг, тасаг..." value={search} onChange={e=>setSearch(e.target.value)}/>
        <select style={{...S.sel,width:160}} value={filterStatus} onChange={e=>setFilterStatus(e.target.value)}><option>All</option>{STATUSES.map(s=><option key={s}>{s}</option>)}</select>
        <select style={{...S.sel,width:180}} value={filterHospital} onChange={e=>setFilterHospital(e.target.value)}><option>All</option>{HOSPITALS.map(h=><option key={h}>{h}</option>)}</select>
        <button style={{...S.btn,padding:"8px 14px",fontSize:11}} onClick={()=>setTab("New Patient")}>+ Шинэ</button>
        <span style={{color:"#475569",fontSize:11}}>{filteredPatients.length} өвчтөн</span>
      </div>
      <div style={{...S.card,padding:0,overflow:"hidden"}}>
        <table style={S.tbl}>
          <thead><tr style={{background:"#0a1120"}}>{["Өвчтөн","Эмнэлэг","Тасаг / Эмч","Аялалын огноо","Статус",""].map(h=><th key={h} style={S.th}>{h}</th>)}</tr></thead>
          <tbody>{filteredPatients.length?filteredPatients.map(p=>(
            <tr key={p.id} style={{background:selectedPatient?.id===p.id?"#1e2d45":"#0d1526",cursor:"pointer"}} onClick={()=>{setSelectedPatient(selectedPatient?.id===p.id?null:p);setDetailTab("Info");}}>
              <td style={S.td}><div style={{fontWeight:700}}>{p.name}</div><div style={{fontSize:10,color:"#475569"}}>{p.phone}</div></td>
              <td style={S.td}><div style={{fontSize:11}}>{p.hospital}</div><div style={{fontSize:10,color:"#475569"}}>📍 {p.hospital_city||"Korea"}</div></td>
              <td style={S.td}><div style={{fontSize:11}}>{p.department}</div><div style={{fontSize:10,color:"#475569"}}>{p.doctor}</div></td>
              <td style={S.td}><div style={{fontSize:11}}>🛬 {fmtDate(p.arrival_date)}</div><div style={{fontSize:11}}>🛫 {fmtDate(p.departure_date)}</div></td>
              <td style={S.td}><span style={S.badge(p.status||"Inquiry")}>{p.status||"Inquiry"}</span></td>
              <td style={S.td} onClick={e=>e.stopPropagation()}><button style={S.bsm("#dc2626")} onClick={()=>deletePatient(p.id)}>Устгах</button></td>
            </tr>
          )):<tr><td colSpan={6} style={{...S.td,textAlign:"center",color:"#475569",padding:32}}>Өвчтөн олдсонгүй.</td></tr>}</tbody>
        </table>
      </div>
      {selectedPatient&&renderDetail(selectedPatient)}
    </>
  );

  // APPOINTMENTS
  const renderAppointments = () => {
    const sorted=[...appointments].sort((a,b)=>a.appt_date>b.appt_date?-1:1).filter(a=>{const pt=patients.find(p=>p.id===a.patient_id);return !search||(pt?.name||"").toLowerCase().includes(search.toLowerCase())||(a.hospital||"").toLowerCase().includes(search.toLowerCase());});
    return(
      <>
        <div style={S.fr}><input style={{...S.inp,width:260}} placeholder="🔍 Өвчтөн, эмнэлэг..." value={search} onChange={e=>setSearch(e.target.value)}/><span style={{color:"#475569",fontSize:11}}>{sorted.length} цаг захиалга</span></div>
        <div style={{...S.card,padding:0,overflow:"hidden"}}>
          <table style={S.tbl}>
            <thead><tr style={{background:"#0a1120"}}>{["Өвчтөн","Эмнэлэг","Тасаг / Эмч","Огноо & Цаг","Статус",""].map(h=><th key={h} style={S.th}>{h}</th>)}</tr></thead>
            <tbody>{sorted.map(a=>{const pt=patients.find(p=>p.id===a.patient_id);return(
              <tr key={a.id} style={{background:"#0d1526"}}>
                <td style={S.td}><div style={{fontWeight:600}}>{pt?.name||"—"}</div></td>
                <td style={S.td}><div style={{fontSize:11}}>{a.hospital||pt?.hospital||"—"}</div></td>
                <td style={S.td}><div>{a.department}</div><div style={{fontSize:10,color:"#475569"}}>{a.doctor}</div></td>
                <td style={S.td}><div>{fmtDate(a.appt_date)}</div><div style={{fontSize:10,color:"#475569"}}>{a.appt_time}</div></td>
                <td style={S.td}><span style={S.badge(a.status)}>{a.status}</span></td>
                <td style={S.td}><div style={{display:"flex",gap:4}}>
                  {["Confirmed","Completed"].filter(st=>st!==a.status).map(st=><button key={st} style={S.bsm(st==="Confirmed"?"#1d4ed8":"#059669")} onClick={async()=>{await sb.patch('appointments',a.id,{status:st});await loadAll();showToast("Шинэчлэгдлээ.");}}>{st}</button>)}
                  <button style={S.bsm("#dc2626")} onClick={async()=>{await sb.del('appointments',a.id);await loadAll();showToast("Устгагдлаа.");}}>Устгах</button>
                </div></td>
              </tr>
            );})}</tbody>
          </table>
        </div>
      </>
    );
  };

  // FOLLOW-UPS
  const renderFollowUps = () => (
    <>
      <div style={S.g2}>
        <div style={S.card}>
          <div style={S.sh}>Тэмдэглэл нэмэх</div>
          <div style={S.fg}><label style={S.lbl}>Өвчтөн</label><select style={S.sel} value={notePatientId} onChange={e=>setNotePatientId(e.target.value)}><option value="">— Сонгоно уу —</option>{patients.map(p=><option key={p.id} value={p.id}>{p.name}</option>)}</select></div>
          <div style={S.fg}><label style={S.lbl}>Тэмдэглэл</label><textarea style={{...S.inp,height:90,resize:"vertical"}} value={noteText} onChange={e=>setNoteText(e.target.value)} placeholder="Шинэчлэлт, мэдэгдэл, дараагийн алхам..."/></div>
          <button style={S.btn} onClick={addNote}>Тэмдэглэл нэмэх</button>
        </div>
        <div style={S.card}>
          <div style={S.sh}>Анхаарал шаардсан өвчтөнүүд</div>
          {patients.filter(p=>["Follow-up","Returned to Mongolia","Treatment Complete"].includes(p.status)).map(p=>(
            <div key={p.id} style={{display:"flex",justifyContent:"space-between",padding:"8px 0",borderBottom:"1px solid #1e2d45"}}>
              <div><div style={{fontWeight:600,fontSize:12}}>{p.name}</div><div style={{fontSize:10,color:"#475569"}}>{p.hospital}</div></div>
              <span style={S.badge(p.status)}>{p.status}</span>
            </div>
          ))}
          {!patients.filter(p=>["Follow-up","Returned to Mongolia","Treatment Complete"].includes(p.status)).length&&<div style={{color:"#475569",fontSize:12}}>Одоохондоо байхгүй.</div>}
        </div>
      </div>
      <div style={{...S.card,marginTop:14}}>
        <div style={S.sh}>Бүх тэмдэглэл</div>
        {[...notes].sort((a,b)=>b.created_at>a.created_at?1:-1).map(n=>{const pt=patients.find(p=>p.id===n.patient_id);return(
          <div key={n.id} style={{display:"flex",gap:12,padding:"9px 0",borderBottom:"1px solid #1e2d45"}}>
            <div style={{background:"#1e2d45",borderRadius:6,padding:"5px 10px",minWidth:100,textAlign:"center",flexShrink:0}}><div style={{fontSize:11,fontWeight:700,color:"#38bdf8"}}>{pt?.name||"—"}</div><div style={{fontSize:9,color:"#475569"}}>{pt?.hospital?.split(" ").slice(0,2).join(" ")}</div></div>
            <div><div style={{fontSize:12,color:"#e2e8f0",lineHeight:1.5}}>{n.text}</div><div style={{fontSize:10,color:"#334155",marginTop:4}}>{fmtDT(n.created_at)}</div></div>
          </div>
        );})}
        {!notes.length&&<div style={{color:"#475569",fontSize:12}}>Тэмдэглэл байхгүй.</div>}
      </div>
    </>
  );

  const renders = {Dashboard:renderDashboard,Inquiries:renderInquiries,"New Patient":renderNewPatient,Patients:renderPatients,Appointments:renderAppointments,"Follow-ups":renderFollowUps};

  return(
    <div style={S.app}>
      <div style={S.sb}>
        <div style={S.lb}>
          <div style={{display:"flex",alignItems:"center",gap:6,marginBottom:4}}><span style={{fontSize:12}}>🇲🇳✈🇰🇷</span></div>
          <div style={{fontWeight:900,fontSize:12,color:"#38bdf8"}}>GEREL MEDI TOUR</div>
          <div style={{fontSize:9,color:"#334155",marginTop:1}}>Mongolia → Korea CRM</div>
        </div>
        <div style={{padding:"8px 0"}}>
          {TABS.map(t=>(
            <button key={t} style={S.nb(tab===t)} onClick={()=>{setTab(t);setSearch("");}}>
              <span style={{fontSize:12}}>{ICONS[t]}</span>{t}
            </button>
          ))}
        </div>
        <div style={{marginTop:"auto",padding:"0 14px"}}>
          <div style={{fontSize:9,color:"#1e2d45",marginBottom:4}}>🗄️ Supabase холбоотой</div>
          <div style={{fontSize:9,color:"#1e2d45"}}>{patients.length} өвчтөн · {appointments.length} цаг · {notes.length} тэмдэглэл</div>
        </div>
      </div>
      <div style={S.main}>
        <div style={{marginBottom:18,display:"flex",justifyContent:"space-between",alignItems:"center"}}>
          <div>
            <div style={{fontSize:18,fontWeight:800,color:"#fff"}}>{tab}</div>
            <div style={{fontSize:11,color:"#475569",marginTop:2}}>{new Date().toLocaleDateString("mn-MN",{weekday:"long",year:"numeric",month:"long",day:"numeric"})}</div>
          </div>
          <button style={{...S.btn,padding:"7px 14px",fontSize:11}} onClick={loadAll}>🔄 Шинэчлэх</button>
        </div>
        {renders[tab]?.()}
      </div>
      {toast&&<div style={S.toast(toast.type)}>{toast.type==="error"?"⚠️":"✅"} {toast.msg}</div>}
    </div>
  );
}
