import { useState } from "react";

const PACKAGES = [
  { id: 1, coins: 100,  price: 15,  bonus: 0,  label: "مبتدئ",   popular: false },
  { id: 2, coins: 500,  price: 70,  bonus: 10, label: "🔥 شعبي", popular: true  },
  { id: 3, coins: 1200, price: 150, bonus: 17, label: "مميز",    popular: false },
  { id: 4, coins: 3500, price: 380, bonus: 30, label: "💎 كبير", popular: false },
  { id: 5, coins: 8000, price: 800, bonus: 38, label: "👑 VIP",  popular: false },
];

const VODAFONE_NUMBER = "01114672635";

export default function PaymentPage() {
  const [selected, setSelected] = useState(PACKAGES[1]);
  const [step, setStep]         = useState(1);
  const [senderPhone, setSenderPhone] = useState("");
  const [senderName, setSenderName]   = useState("");
  const [loading, setLoading]         = useState(false);
  const [done, setDone]               = useState(false);
  const [error, setError]             = useState("");

  const handleConfirm = () => {
    setError("");
    if (!senderPhone || senderPhone.length < 11) {
      setError("ادخل رقم موبايلك الصح (11 رقم)");
      return;
    }
    if (!senderName.trim()) {
      setError("ادخل اسمك عشان نتعرف عليك");
      return;
    }
    setLoading(true);
    setTimeout(() => {
      setLoading(false);
      setDone(true);
    }, 1500);
  };

  const s = {
    page: {
      minHeight: "100vh",
      background: "#050505",
      fontFamily: "'Tajawal', sans-serif",
      direction: "rtl",
      display: "flex",
      alignItems: "center",
      justifyContent: "center",
      padding: "20px",
      backgroundImage: "radial-gradient(ellipse at 20% 20%, rgba(255,0,102,0.07) 0%, transparent 50%), radial-gradient(ellipse at 80% 80%, rgba(124,58,237,0.07) 0%, transparent 50%)",
    },
    wrap: { width: "100%", maxWidth: 400 },
    header: { textAlign: "center", marginBottom: 24 },
    logo: { fontSize: 44, marginBottom: 4 },
    title: { fontSize: 26, fontWeight: 900, letterSpacing: 6, background: "linear-gradient(135deg,#FF0066,#7C3AED)", WebkitBackgroundClip: "text", WebkitTextFillColor: "transparent" },
    sub: { color: "#555", fontSize: 13, marginTop: 4 },
    card: { background: "#111", borderRadius: 24, border: "1px solid #1e1e1e", overflow: "hidden" },
    stepsBar: { display: "flex", borderBottom: "1px solid #1e1e1e" },
    stepItem: (active, done) => ({
      flex: 1, padding: "13px 8px", textAlign: "center", fontSize: 12, fontWeight: 700,
      color: done ? "#00D084" : active ? "#FF0066" : "#444",
      borderBottom: active ? "2px solid #FF0066" : "2px solid transparent",
      transition: "all 0.3s",
    }),
    body: { padding: 22 },
    sectionTitle: { color: "#fff", fontSize: 15, fontWeight: 800, marginBottom: 14 },
    pkg: (sel) => ({
      borderRadius: 14, border: `2px solid ${sel ? "#FF0066" : "#1e1e1e"}`,
      cursor: "pointer", overflow: "hidden", position: "relative",
      background: sel ? "rgba(255,0,102,0.05)" : "transparent",
      transition: "all 0.2s", marginBottom: 8,
    }),
    pkgBadge: { background: "linear-gradient(90deg,#FF0066,#7C3AED)", color: "#fff", fontSize: 10, fontWeight: 800, textAlign: "center", padding: "3px 0" },
    pkgRow: (pop) => ({ display: "flex", alignItems: "center", justifyContent: "space-between", padding: pop ? "16px 14px 12px" : "12px 14px" }),
    coins: { color: "#FFD700", fontSize: 17, fontWeight: 900 },
    bonus: { background: "rgba(0,208,132,0.15)", color: "#00D084", fontSize: 10, fontWeight: 700, padding: "2px 7px", borderRadius: 8, marginRight: 6 },
    pkgLabel: { color: "#555", fontSize: 11, marginTop: 2 },
    pkgPrice: (sel) => ({ fontSize: 18, fontWeight: 900, color: sel ? "#FF0066" : "#fff" }),
    btn: { width: "100%", padding: 15, borderRadius: 14, border: "none", background: "linear-gradient(135deg,#FF0066,#7C3AED)", color: "#fff", fontSize: 15, fontWeight: 800, cursor: "pointer", marginTop: 16 },
    btnGray: { width: "100%", padding: 13, borderRadius: 14, border: "1px solid #2a2a2a", background: "transparent", color: "#888", fontSize: 14, fontWeight: 700, cursor: "pointer", marginTop: 10 },
    // Vodafone box
    vfBox: { background: "rgba(255,0,0,0.08)", border: "1px solid rgba(255,0,0,0.25)", borderRadius: 18, padding: 20, textAlign: "center", marginBottom: 18 },
    vfIcon: { fontSize: 44, marginBottom: 8 },
    vfTitle: { color: "#fff", fontSize: 15, fontWeight: 800, marginBottom: 6 },
    vfSteps: { color: "#888", fontSize: 13, lineHeight: 1.8, marginBottom: 12 },
    vfNumber: { background: "rgba(255,0,0,0.15)", borderRadius: 12, padding: "12px 0", marginTop: 8 },
    vfNumberText: { color: "#FF3333", fontSize: 26, fontWeight: 900, letterSpacing: 3 },
    vfCopy: { color: "#888", fontSize: 11, marginTop: 4 },
    // Amount box
    amtBox: { background: "#1a1a1a", borderRadius: 14, padding: 14, marginBottom: 16 },
    amtRow: { display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 6 },
    amtLabel: { color: "#666", fontSize: 13 },
    amtVal: { color: "#fff", fontWeight: 700, fontSize: 13 },
    amtTotal: { color: "#FF0066", fontWeight: 900, fontSize: 20 },
    divider: { height: 1, background: "#2a2a2a", margin: "10px 0" },
    // Input
    inputGroup: { marginBottom: 14 },
    inputLabel: { color: "#888", fontSize: 13, marginBottom: 6, display: "block" },
    input: { width: "100%", background: "#1a1a1a", border: "1px solid #2a2a2a", borderRadius: 12, padding: "13px 14px", color: "#fff", fontFamily: "Tajawal,sans-serif", fontSize: 15, outline: "none", boxSizing: "border-box" },
    errorMsg: { color: "#FF3B3B", fontSize: 13, textAlign: "center", marginTop: 8 },
    // Success
    successBox: { textAlign: "center", padding: "10px 0" },
    successIcon: { fontSize: 64, marginBottom: 12 },
    successTitle: { color: "#fff", fontSize: 22, fontWeight: 900, marginBottom: 6 },
    successSub: { color: "#888", fontSize: 14, marginBottom: 20 },
    coinsBox: { background: "rgba(255,215,0,0.1)", border: "1px solid rgba(255,215,0,0.2)", borderRadius: 16, padding: 18, marginBottom: 20 },
    coinsNum: { color: "#FFD700", fontSize: 34, fontWeight: 900 },
    coinsLabel: { color: "#888", fontSize: 13, marginTop: 4 },
    noteBox: { background: "rgba(255,0,102,0.08)", border: "1px solid rgba(255,0,102,0.2)", borderRadius: 14, padding: 14, marginBottom: 16 },
    noteText: { color: "#aaa", fontSize: 12, lineHeight: 1.8 },
    footer: { textAlign: "center", marginTop: 18, color: "#2a2a2a", fontSize: 11 },
  };

  return (
    <div style={s.page}>
      <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800;900&display=swap" rel="stylesheet" />
      <div style={s.wrap}>

        {/* Header */}
        <div style={s.header}>
          <div style={s.logo}>🌀</div>
          <div style={s.title}>VORTEX</div>
          <div style={s.sub}>شحن كوينز 🪙</div>
        </div>

        <div style={s.card}>
          {/* Steps */}
          <div style={s.stepsBar}>
            {["اختار الباقة", "تحويل فودافون", "تأكيد"].map((label, i) => (
              <div key={i} style={s.stepItem(step === i+1, step > i+1)}>
                {step > i+1 ? "✓ " : `${i+1}. `}{label}
              </div>
            ))}
          </div>

          <div style={s.body}>

            {/* ══ STEP 1: اختار الباقة ══ */}
            {step === 1 && !done && (
              <div>
                <div style={s.sectionTitle}>اختار الباقة المناسبة 👇</div>
                {PACKAGES.map(pkg => (
                  <div key={pkg.id} style={s.pkg(selected.id === pkg.id)} onClick={() => setSelected(pkg)}>
                    {pkg.popular && <div style={s.pkgBadge}>⭐ الأكثر مبيعاً</div>}
                    <div style={s.pkgRow(pkg.popular)}>
                      <div>
                        <div style={{ display: "flex", alignItems: "center", gap: 6 }}>
                          <span style={s.coins}>🪙 {pkg.coins.toLocaleString()}</span>
                          {pkg.bonus > 0 && <span style={s.bonus}>+{pkg.bonus}% مجاناً</span>}
                        </div>
                        <div style={s.pkgLabel}>{pkg.label}</div>
                      </div>
                      <div style={s.pkgPrice(selected.id === pkg.id)}>{pkg.price} جنيه</div>
                    </div>
                  </div>
                ))}
                <button style={s.btn} onClick={() => setStep(2)}>
                  التالي ← ({selected.price} جنيه)
                </button>
              </div>
            )}

            {/* ══ STEP 2: تعليمات فودافون كاش ══ */}
            {step === 2 && !done && (
              <div>
                <div style={s.vfBox}>
                  <div style={s.vfIcon}>📱</div>
                  <div style={s.vfTitle}>حول عن طريق فودافون كاش</div>
                  <div style={s.vfSteps}>
                    1️⃣ افتح تطبيق فودافون كاش<br/>
                    2️⃣ اضغط "تحويل أموال"<br/>
                    3️⃣ ادخل الرقم ده 👇
                  </div>
                  <div style={s.vfNumber}>
                    <div style={s.vfNumberText}>{VODAFONE_NUMBER}</div>
                    <div style={s.vfCopy}>اضغط للنسخ</div>
                  </div>
                </div>

                {/* ملخص */}
                <div style={s.amtBox}>
                  <div style={s.amtRow}>
                    <span style={s.amtLabel}>الباقة</span>
                    <span style={s.amtVal}>🪙 {selected.coins.toLocaleString()} كوين</span>
                  </div>
                  <div style={s.divider} />
                  <div style={s.amtRow}>
                    <span style={s.amtLabel}>المبلغ اللي هتحوله</span>
                    <span style={s.amtTotal}>{selected.price} جنيه</span>
                  </div>
                </div>

                {/* بيانات المحول */}
                <div style={s.sectionTitle}>بياناتك عشان نأكد التحويل 👇</div>
                <div style={s.inputGroup}>
                  <label style={s.inputLabel}>رقم موبايلك (اللي حولت منه)</label>
                  <input
                    style={s.input}
                    placeholder="01XXXXXXXXX"
                    value={senderPhone}
                    onChange={e => setSenderPhone(e.target.value)}
                    maxLength={11}
                    type="tel"
                  />
                </div>
                <div style={s.inputGroup}>
                  <label style={s.inputLabel}>اسمك</label>
                  <input
                    style={s.input}
                    placeholder="اسمك الكامل"
                    value={senderName}
                    onChange={e => setSenderName(e.target.value)}
                  />
                </div>

                {error && <div style={s.errorMsg}>⚠️ {error}</div>}

                <button style={s.btn} onClick={handleConfirm} disabled={loading}>
                  {loading ? "⏳ جاري التأكيد..." : "✅ أكدت التحويل"}
                </button>
                <button style={s.btnGray} onClick={() => setStep(1)}>← رجوع</button>
              </div>
            )}

            {/* ══ STEP 3 / SUCCESS ══ */}
            {done && (
              <div style={s.successBox}>
                <div style={s.successIcon}>🎉</div>
                <div style={s.successTitle}>طلبك اتسجل!</div>
                <div style={s.successSub}>هنراجع التحويل ونضيف الكوينز خلال 30 دقيقة</div>

                <div style={s.coinsBox}>
                  <div style={s.coinsNum}>🪙 {selected.coins.toLocaleString()}</div>
                  <div style={s.coinsLabel}>كوين هيتضافوا لحسابك</div>
                </div>

                <div style={s.noteBox}>
                  <div style={s.noteText}>
                    📋 <strong style={{color:"#fff"}}>بياناتك:</strong><br/>
                    الرقم: {senderPhone}<br/>
                    الاسم: {senderName}<br/>
                    المبلغ: {selected.price} جنيه<br/>
                    الكوينز: {selected.coins.toLocaleString()} 🪙<br/><br/>
                    ⏰ وقت المراجعة: خلال 30 دقيقة<br/>
                    📞 للاستفسار: {VODAFONE_NUMBER}
                  </div>
                </div>

                <button style={s.btn} onClick={() => { setDone(false); setStep(1); setSenderPhone(""); setSenderName(""); }}>
                  شحن تاني 🌀
                </button>
              </div>
            )}

          </div>
        </div>

        <div style={s.footer}>🔒 VORTEX © 2025 • جميع الحقوق محفوظة</div>
      </div>
    </div>
  );
}
