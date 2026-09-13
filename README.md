<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Fresh Yogurt — บัตรสะสมคะแนน</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jsQR/1.4.0/jsQR.js"></script>
<script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
<script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
<style>
  :root{
    --blue:#2F9BEA;
    --blue-dark:#1E7FC4;
    --blue-deep:#1768A8;
    --navy:#003F80;
    --bg:#F3F5F7;
    --ink:#161A1F;
    --sub:#8A8F98;
    --line:#E7E9EC;
    --green:#06C755;
    --red:#E14B4B;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;background:#DCE1E6;font-family:-apple-system,'Segoe UI',Helvetica,Arial,sans-serif;}
  .phone{max-width:430px;margin:0 auto;min-height:100vh;background:var(--bg);position:relative;overflow-x:hidden;}
  button{font-family:inherit;cursor:pointer;}
  input,select,textarea{font-family:inherit;}

  .pagehead{
    display:flex;align-items:center;justify-content:center;position:relative;
    padding:18px 16px 14px;background:#fff;font-weight:700;font-size:1.02rem;color:var(--ink);border-bottom:1px solid var(--line);
  }
  .pagehead .back{position:absolute;left:14px;background:none;border:none;color:var(--ink);display:flex;align-items:center;}
  .pagehead .back svg{width:22px;height:22px;}

  /* ================= LOGIN ================= */
  .login-wrap{background:linear-gradient(180deg,var(--blue) 0%, var(--blue-dark) 55%);min-height:100vh;padding-top:70px;}
  .login-card{background:#fff;border-radius:22px 22px 0 0;margin-top:150px;padding:36px 26px 46px;text-align:center;min-height:calc(100vh - 220px);}
  .avatar-placeholder{
    width:96px;height:96px;border-radius:50%;background:var(--navy);border:4px solid #fff;
    margin:-110px auto 22px;display:flex;align-items:center;justify-content:center;overflow:hidden;
    box-shadow:0 2px 10px rgba(0,0,0,0.12);
  }
  .avatar-placeholder img{width:100%;height:100%;object-fit:cover;}
  .login-card h1{font-size:1.25rem;margin:0 0 10px;}
  .login-card p.sub{color:var(--sub);font-size:0.9rem;line-height:1.5;margin:0 0 26px;}
  .tel-input{width:100%;border:1.5px solid var(--line);border-radius:10px;padding:15px 16px;font-size:1rem;outline:none;margin-bottom:18px;background:#FAFBFC;}
  .tel-input:focus{border-color:var(--blue);}
  .btn-primary{width:100%;background:var(--blue);color:#fff;border:none;border-radius:10px;padding:15px;font-size:1rem;font-weight:700;}
  .btn-primary:disabled{background:#BFD9EF;}
  .btn-primary:hover:not(:disabled){background:var(--blue-dark);}
  .divider{display:flex;align-items:center;gap:12px;color:var(--sub);font-size:0.85rem;margin:22px 0;}
  .divider::before,.divider::after{content:"";flex:1;height:1px;background:var(--line);}
  .btn-line{width:100%;background:#F1F2F4;border:none;border-radius:10px;padding:14px;font-size:0.98rem;font-weight:700;color:#222;display:flex;align-items:center;justify-content:center;gap:10px;}
  .line-badge{background:var(--green);color:#fff;font-size:0.66rem;font-weight:800;border-radius:5px;padding:3px 6px;letter-spacing:0.02em;}
  .line-inline{margin-top:14px;display:flex;gap:8px;}
  .line-inline input{
    flex:1;border:1.5px solid var(--line);border-radius:9px;padding:10px 12px;font-size:0.9rem;outline:none;
  }
  .line-inline input:focus{border-color:var(--green);}
  .line-inline button{background:var(--green);color:#fff;border:none;border-radius:9px;padding:0 16px;font-size:0.85rem;font-weight:700;}
  .setup-note{font-size:0.76rem;color:var(--sub);margin-top:10px;line-height:1.5;text-align:left;background:#F6F7F9;border-radius:9px;padding:10px 12px;}
  .dev-note{font-size:0.8rem;color:#8A6D1D;background:#FFF6DC;border:1px solid #F0DFA0;border-radius:10px;padding:12px 14px;text-align:left;margin-bottom:20px;}
  .dev-note b{letter-spacing:0.06em;}

  /* ================= OTP ================= */
  .otp-card{background:#fff;border-radius:22px;margin:26px 18px;padding:40px 24px;text-align:center;}
  .otp-card h1{font-size:1.15rem;margin:0 0 12px;}
  .otp-card p.sub{color:var(--sub);font-size:0.88rem;line-height:1.5;margin:0 0 26px;}
  .otp-boxes{display:flex;gap:10px;justify-content:center;margin-bottom:22px;}
  .otp-boxes input{width:44px;height:52px;text-align:center;font-size:1.3rem;border-radius:10px;border:1.5px solid var(--line);outline:none;}
  .otp-boxes input:focus{border-color:var(--blue);}
  .otp-meta{font-size:0.85rem;color:var(--sub);margin-bottom:26px;}
  .otp-meta a{color:var(--blue);text-decoration:underline;cursor:pointer;}

  /* ================= HOME ================= */
  .home-header{background:linear-gradient(135deg,var(--blue) 0%, var(--blue-deep) 100%);padding:20px 18px 62px;color:#fff;}
  .home-header .brandrow{display:flex;align-items:center;gap:12px;}
  .home-header .brand-avatar{
    width:50px;height:50px;border-radius:50%;background:var(--navy);display:flex;align-items:center;justify-content:center;
    flex:none;overflow:hidden;border:2px solid rgba(255,255,255,0.6);
  }
  .home-header .brand-avatar img{width:100%;height:100%;object-fit:cover;}
  .home-header .brandname{font-weight:800;font-size:1.08rem;}
  .home-header .branch{font-size:0.78rem;color:#DCEEFB;margin-top:2px;}
  .header-iconbtn{
    margin-left:auto;width:38px;height:38px;border-radius:50%;background:rgba(255,255,255,0.2);border:none;
    display:flex;align-items:center;justify-content:center;color:#fff;flex:none;
  }
  .header-iconbtn svg{width:19px;height:19px;}
  .header-iconbtn:hover{background:rgba(255,255,255,0.32);}

  .member-card{
    background:#fff;border-radius:16px;padding:18px 18px;margin:-40px 16px 0;box-shadow:0 6px 20px rgba(20,60,100,0.12);
    display:flex;align-items:center;justify-content:space-between;
  }
  .member-card .name{font-weight:800;font-size:1.05rem;}
  .member-card .phone{font-size:0.82rem;color:var(--sub);margin-top:5px;}
  .pts-badge{text-align:center;}
  .pts-badge .num{font-size:1.5rem;font-weight:800;color:var(--blue);display:flex;align-items:center;gap:5px;justify-content:flex-end;}
  .pts-badge .lbl{font-size:0.72rem;color:var(--sub);margin-top:2px;}
  .pchip{width:20px;height:20px;border-radius:50%;background:var(--blue);color:#fff;font-size:0.65rem;font-weight:800;display:inline-flex;align-items:center;justify-content:center;flex:none;}

  .section-title-row{display:flex;align-items:center;justify-content:space-between;padding:26px 18px 12px;}
  .section-title-row h2{font-size:1.02rem;margin:0;font-weight:800;}
  .section-title-row .addbtn{background:var(--blue);color:#fff;border:none;border-radius:8px;padding:7px 13px;font-size:0.8rem;font-weight:700;}
  .section-title-row .addbtn:hover{background:var(--blue-dark);}

  .coupon-list{padding:0 16px 20px;display:flex;flex-direction:column;gap:14px;}
  .coupon-card{background:#fff;border-radius:14px;overflow:hidden;box-shadow:0 2px 8px rgba(20,40,70,0.06);display:flex;}
  .coupon-img{width:118px;flex:none;background:linear-gradient(135deg,#FBD5D5,#F5A9BE);display:flex;align-items:center;justify-content:center;position:relative;}
  .coupon-img img{width:100%;height:100%;object-fit:cover;}
  .coupon-body{padding:12px 14px;flex:1;min-width:0;}
  .coupon-body .ttl{font-weight:800;font-size:0.94rem;margin-bottom:4px;}
  .coupon-body .desc{font-size:0.78rem;color:var(--sub);margin-bottom:6px;overflow:hidden;text-overflow:ellipsis;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;}
  .coupon-body .expiry{font-size:0.75rem;color:var(--sub);margin-bottom:8px;}
  .coupon-body .bottomrow{display:flex;align-items:center;justify-content:space-between;}
  .cost{color:var(--blue);font-weight:800;font-size:0.9rem;display:flex;align-items:center;gap:6px;}
  .rowicons{display:flex;gap:6px;}
  .icobtn{background:none;border:1px solid var(--line);border-radius:7px;width:28px;height:28px;display:flex;align-items:center;justify-content:center;}
  .icobtn svg{width:14px;height:14px;color:var(--sub);}
  .icobtn:hover{border-color:var(--blue);}
  .icobtn.danger:hover{border-color:var(--red);}
  .icobtn.danger:hover svg{color:var(--red);}
  .redeembtn{background:var(--blue);color:#fff;border:none;border-radius:7px;padding:6px 12px;font-size:0.78rem;font-weight:700;}
  .redeembtn:disabled{background:#CBD8E3;}

  .empty{color:var(--sub);text-align:center;padding:40px 20px;font-size:0.88rem;}
  .empty svg{width:52px;height:52px;color:#D3D8DD;margin-bottom:12px;}

  /* ---------- sheet overlay (coupon add/edit) ---------- */
  .sheet-backdrop{position:fixed;inset:0;background:rgba(15,20,25,0.42);display:flex;align-items:flex-end;z-index:50;}
  .sheet{background:#fff;width:100%;max-width:430px;margin:0 auto;border-radius:20px 20px 0 0;padding:22px 20px 26px;max-height:88vh;overflow-y:auto;}
  .sheet h3{margin:0 0 16px;font-size:1.05rem;}
  .field{margin-bottom:14px;}
  .field label{display:block;font-size:0.8rem;color:var(--sub);margin-bottom:6px;}
  .field input[type=text],.field input[type=number],.field input[type=date],.field input[type=password],.field select,.field textarea{
    width:100%;border:1.5px solid var(--line);border-radius:9px;padding:10px 12px;font-size:0.92rem;outline:none;
  }
  .field input:focus,.field select:focus,.field textarea:focus{border-color:var(--blue);}
  .field textarea{resize:vertical;min-height:60px;}
  .imgpick{display:flex;align-items:center;gap:12px;}
  .imgpick .preview{width:64px;height:64px;border-radius:10px;object-fit:cover;background:#F1F3F5;flex:none;display:flex;align-items:center;justify-content:center;color:var(--sub);font-size:0.7rem;text-align:center;}
  .imgpick label.upl{border:1.5px dashed var(--line);border-radius:9px;padding:9px 14px;font-size:0.82rem;color:var(--sub);}
  .sheet-actions{display:flex;gap:10px;margin-top:20px;}
  .sheet-actions button{flex:1;border-radius:10px;padding:12px;font-size:0.92rem;font-weight:700;border:none;}
  .sheet-actions .cancel{background:#F1F2F4;color:var(--ink);}
  .sheet-actions .save{background:var(--blue);color:#fff;}

  /* ================= MEMBERSHIP CARD (QR) ================= */
  .qr-wrap{padding:26px 20px;}
  .qr-card{background:linear-gradient(180deg,var(--blue) 0%, var(--blue-dark) 100%);border-radius:20px;padding:26px 20px 30px;}
  .qr-inner{background:#fff;border-radius:16px;padding:26px 20px;text-align:center;}
  .qr-avatar{
    width:70px;height:70px;border-radius:50%;margin:-58px auto 14px;background:var(--navy);border:4px solid #fff;
    display:flex;align-items:center;justify-content:center;box-shadow:0 2px 8px rgba(0,0,0,0.1);overflow:hidden;
  }
  .qr-avatar img{width:100%;height:100%;object-fit:cover;}
  .qr-name{font-weight:800;font-size:1.1rem;margin-bottom:16px;}
  .qr-box{position:relative;width:230px;height:230px;margin:0 auto 16px;display:flex;align-items:center;justify-content:center;}
  .qr-box img,.qr-box canvas,.qr-box table{width:230px !important;height:230px !important;}
  .qr-center{
    position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);width:40px;height:40px;border-radius:50%;
    background:var(--blue);display:flex;align-items:center;justify-content:center;box-shadow:0 0 0 4px #fff;
  }
  .qr-center svg{width:20px;height:20px;color:#fff;}
  .qr-caption{font-size:0.85rem;color:var(--ink);}
  .qr-key{font-size:0.72rem;color:var(--sub);margin-top:8px;letter-spacing:0.03em;}

  /* ================= ACCOUNT ================= */
  .acct-wrap{padding:22px 18px;}
  .acct-row{display:flex;justify-content:space-between;padding:14px 4px;border-bottom:1px solid var(--line);font-size:0.92rem;}
  .acct-row span:first-child{color:var(--sub);}
  .acct-actions{margin-top:22px;display:flex;flex-direction:column;gap:10px;}

  /* ================= POINTS HISTORY ================= */
  .hist-headcard{background:linear-gradient(135deg,var(--blue) 0%, var(--blue-deep) 100%);padding:0 18px 34px;}
  .hist-card{background:#fff;border-radius:14px;padding:20px;text-align:center;box-shadow:0 4px 14px rgba(0,0,0,0.08);}
  .hist-card .lbl{font-size:0.82rem;color:var(--sub);margin-bottom:8px;}
  .hist-card .num{font-size:1.6rem;font-weight:800;display:flex;align-items:center;justify-content:center;gap:8px;}
  .hist-tabs{display:flex;background:#fff;border-bottom:1px solid var(--line);}
  .hist-tabs button{flex:1;background:none;border:none;padding:14px 4px;font-size:0.86rem;font-weight:600;color:var(--sub);border-bottom:2.5px solid transparent;}
  .hist-tabs button.active{color:var(--blue);border-bottom-color:var(--blue);font-weight:700;}
  .hist-list{padding:6px 18px 20px;}
  .hist-item{display:flex;justify-content:space-between;align-items:center;padding:13px 0;border-bottom:1px solid var(--line);}
  .hist-item .note{font-size:0.9rem;font-weight:600;}
  .hist-item .date{font-size:0.76rem;color:var(--sub);margin-top:2px;}
  .hist-item .amt{font-weight:800;font-size:0.95rem;}
  .hist-item .amt.earn{color:var(--green);}
  .hist-item .amt.use{color:var(--red);}

  /* ================= ADMIN ================= */
  .admin-lock{padding:60px 26px;text-align:center;}
  .admin-lock .lockicon{width:64px;height:64px;border-radius:50%;background:#EAF3FB;display:flex;align-items:center;justify-content:center;margin:0 auto 18px;color:var(--blue);}
  .admin-lock .lockicon svg{width:30px;height:30px;}
  .admin-lock h1{font-size:1.1rem;margin:0 0 8px;}
  .admin-lock p{color:var(--sub);font-size:0.86rem;margin:0 0 22px;}
  .admin-panel{padding:20px 18px 30px;}
  .admin-panel .toolbox{background:#fff;border-radius:14px;padding:16px;margin-bottom:20px;box-shadow:0 2px 8px rgba(20,40,70,0.06);}
  .admin-panel .toolbox h3{margin:0 0 10px;font-size:0.92rem;}
  .admin-panel .toolrow{display:flex;gap:10px;flex-wrap:wrap;}
  .admin-panel .toolrow button{border:1px solid var(--line);background:#fff;border-radius:8px;padding:9px 13px;font-size:0.82rem;font-weight:600;color:var(--ink);}
  .admin-panel .toolrow button:hover{border-color:var(--blue);color:var(--blue-dark);}
  .admin-panel .toolrow button.primary{background:var(--blue);color:#fff;border-color:var(--blue);}
  .admin-badge{display:inline-flex;align-items:center;gap:6px;background:#EAF3FB;color:var(--blue-dark);font-size:0.76rem;font-weight:700;padding:5px 11px;border-radius:20px;margin-bottom:16px;}

  /* ---------- QR scanner overlay ---------- */
  .scan-overlay{position:fixed;inset:0;background:rgba(10,14,18,0.9);z-index:80;display:flex;align-items:center;justify-content:center;padding:20px;}
  .scan-box{background:#fff;border-radius:16px;padding:18px;width:100%;max-width:380px;}
  .scan-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;}
  .scan-head span{font-weight:700;}
  .scan-head button{background:none;border:none;color:var(--sub);}
  .scan-head button svg{width:20px;height:20px;}
  .scan-note{font-size:0.78rem;color:var(--sub);margin-top:8px;}
  .found-card{background:#F6FAFD;border-radius:12px;padding:14px;margin-top:14px;}
  .found-card .fname{font-weight:800;font-size:0.98rem;}
  .found-card .fmeta{font-size:0.8rem;color:var(--sub);margin:3px 0 12px;}
  .found-row{display:flex;gap:8px;margin-bottom:10px;}
  .found-row input,.found-row select{flex:1;border:1.5px solid var(--line);border-radius:8px;padding:8px 10px;font-size:0.85rem;}
  .found-row button{background:var(--blue);color:#fff;border:none;border-radius:8px;padding:0 14px;font-size:0.82rem;font-weight:700;}

  /* ================= BOTTOM NAV ================= */
  .bottom-nav{position:sticky;bottom:0;left:0;right:0;background:#fff;border-top:1px solid var(--line);display:flex;padding:9px 0 12px;}
  .bottom-nav button{flex:1;background:none;border:none;display:flex;flex-direction:column;align-items:center;gap:4px;color:var(--sub);font-size:0.68rem;font-weight:600;}
  .bottom-nav button svg{width:21px;height:21px;}
  .bottom-nav button.active{color:var(--blue);}
  .content-scroll{padding-bottom:6px;}
</style>
</head>
<body>
<div class="phone" id="phoneRoot"><div id="app"></div></div>

<script>
(function(){
"use strict";

const LOGO = "data:image/png;base64,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";
const BRAND_NAME = "Fresh Yogurt";
const BRANCH_NAME = "สาขาหน้ามหาวิทยาลัยมหิดล";
const ADMIN_PASSWORD = "Greekzly888";
const QR_PREFIX = "FRESHYOGURT|";
const QR_USE_PREFIX = "FRESHYOGURT-USE|";

/* ====== เชื่อมต่อระบบจริง (กรอกค่าของร้านเองที่นี่) ======
   LIFF_ID: มี 3 ชุดตามขั้นตอนของ LINE Mini App (Developing / Review / Published)
            แต่ละชุดจะใช้งานได้จริงก็ต่อเมื่อ "Endpoint URL" ที่ตั้งไว้ใน LINE Developers Console
            ของชาแนลนั้นๆ ตรงกับโดเมนจริงที่ไฟล์นี้ถูกอัปโหลดไปโฮสต์ไว้ (ต้องเป็น https)
            เปลี่ยนตัวแปร ACTIVE_LIFF_ENV ด้านล่างเป็น "developing" / "review" / "published"
            เพื่อสลับว่าจะให้ใช้ชุดไหนตอนนี้
   SMS_SEND_ENDPOINT: ที่อยู่ API ฝั่งเซิร์ฟเวอร์ของร้าน (ต้องทำแยกต่างหาก) ที่จะยิงคำสั่งส่ง SMS OTP
            ผ่านผู้ให้บริการ เช่น Twilio / THSMS / DeeSMSx เนื่องจากคีย์ลับของผู้ให้บริการ SMS
            ห้ามฝังไว้ในไฟล์ HTML ฝั่งไคลเอนต์โดยตรง จึงต้องมีเซิร์ฟเวอร์กลางเป็นตัวส่งแทน
   ======================================================= */
const LIFF_IDS = {
  developing: "2011578364-5e9VdvlV",
  review:     "2011578365-zMPzIpVe",
  published:  "2011578366-mQ3R0Bwa"
};
const ACTIVE_LIFF_ENV = "published"; // เปลี่ยนเป็น "developing" หรือ "review" เวลาทดสอบก่อนขึ้นจริง
const LIFF_ID = LIFF_IDS[ACTIVE_LIFF_ENV] || "";
const SMS_SEND_ENDPOINT = "";    // เช่น "https://your-backend.example.com/api/send-otp"

const ICONS = {
  user: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.5-7 8-7s8 3 8 7"/></svg>`,
  home: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M4 11l8-7 8 7"/><path d="M6 10v9h12v-9"/></svg>`,
  ticket: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M3 9a2 2 0 012-2h14a2 2 0 012 2v1a2 2 0 000 4v1a2 2 0 01-2 2H5a2 2 0 01-2-2v-1a2 2 0 000-4z"/></svg>`,
  card: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="3" y="6" width="18" height="13" rx="2"/><path d="M3 10h18"/><path d="M7 15h4"/></svg>`,
  edit: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 20h9"/><path d="M16.5 3.5a2.1 2.1 0 013 3L7 19l-4 1 1-4z"/></svg>`,
  trash: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 7h16"/><path d="M10 11v6"/><path d="M14 11v6"/><path d="M6 7l1 13h10l1-13"/><path d="M9 7V4h6v3"/></svg>`,
  star: `<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2l2.9 6.6 7.1.6-5.4 4.7 1.7 7-6.3-3.9-6.3 3.9 1.7-7L2 9.2l7.1-.6z"/></svg>`,
  gear: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.7 1.7 0 00.3 1.9l.1.1a2 2 0 11-2.8 2.8l-.1-.1a1.7 1.7 0 00-1.9-.3 1.7 1.7 0 00-1 1.5V21a2 2 0 01-4 0v-.1a1.7 1.7 0 00-1-1.6 1.7 1.7 0 00-1.9.3l-.1.1a2 2 0 11-2.8-2.8l.1-.1a1.7 1.7 0 00.3-1.9 1.7 1.7 0 00-1.5-1H3a2 2 0 010-4h.1a1.7 1.7 0 001.5-1 1.7 1.7 0 00-.3-1.9l-.1-.1a2 2 0 112.8-2.8l.1.1a1.7 1.7 0 001.9.3H9a1.7 1.7 0 001-1.5V3a2 2 0 014 0v.1a1.7 1.7 0 001 1.5 1.7 1.7 0 001.9-.3l.1-.1a2 2 0 112.8 2.8l-.1.1a1.7 1.7 0 00-.3 1.9V9a1.7 1.7 0 001.5 1H21a2 2 0 010 4h-.1a1.7 1.7 0 00-1.5 1z"/></svg>`,
  lock: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="5" y="11" width="14" height="9" rx="2"/><path d="M8 11V7a4 4 0 018 0v4"/></svg>`,
  history: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="4" y="4" width="12" height="16" rx="2"/><path d="M7 8h6M7 11.5h6M7 15h3"/><circle cx="18" cy="17" r="4.2"/><path d="M18 15.2v1.9l1.3 1"/></svg>`,
  close: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M6 6l12 12M18 6L6 18"/></svg>`,
  back: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 18l-6-6 6-6"/></svg>`,
  searchdoc: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.4"><rect x="4" y="3" width="13" height="17" rx="2"/><path d="M7 7.5h7M7 11h7M7 14.5h4"/><circle cx="17" cy="17" r="4.3"/><path d="M20.2 20.2L22 22"/></svg>`
};

const DEFAULT_COUPONS = [
  {id:"c1", image:null, title:"แลกฟรีส่วนลด 10 บาท", desc:"ใช้ได้กับสินค้าทุกรายการหน้าร้าน 1 รายการ", cost:15, expiry:"2026-12-31"},
  {id:"c2", image:null, title:"แลกฟรีส่วนลด 20 บาท", desc:"ใช้ได้กับสินค้าทุกรายการหน้าร้าน 1 รายการ", cost:30, expiry:"2026-12-31"},
  {id:"c3", image:null, title:"แลกฟรีส่วนลด 30 บาท", desc:"ใช้ได้กับสินค้าทุกรายการหน้าร้าน 1 รายการ", cost:45, expiry:"2026-12-31"}
];

let state = {
  screen: "login",
  phone: "",
  members: {},
  customer: null,
  sessionKey: null,
  coupons: [],
  activeTab: "home",
  isAdmin: false,
  adminError: "",
  historyFilter: "all",
  scanStream: null,
  scanRAF: null,
  scanFoundKey: null,
  pendingOtp: null,
  otpError: "",
  liffReady: false,
  liffFailed: false
};

const app = document.getElementById("app");

function todayStr(){ return new Date().toISOString().slice(0,10); }
function fmtDate(d){
  if(!d) return "—";
  try{ return new Date(d+"T00:00:00").toLocaleDateString("th-TH",{year:"numeric",month:"short",day:"numeric"}); }
  catch(e){ return d; }
}
function fmtDateTime(d){
  if(!d) return "—";
  try{ return new Date(d).toLocaleString("th-TH",{year:"numeric",month:"short",day:"numeric",hour:"2-digit",minute:"2-digit"}); }
  catch(e){ return d; }
}
function esc(s){ return String(s==null?"":s).replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c])); }
function uid(){ return "c"+Date.now().toString(36)+Math.random().toString(36).slice(2,6); }
function addDays(dateStr, days){ const d = new Date(dateStr+"T00:00:00"); d.setDate(d.getDate()+days); return d.toISOString().slice(0,10); }
function isPhone(v){ return /^0[0-9]{9}$/.test(v); }
function memberKey(identifier){ return isPhone(identifier) ? identifier : "line:"+identifier.trim(); }
function sixDigit(){ return String(Math.floor(100000 + Math.random()*900000)); }
async function sendSmsIfConfigured(phone, code){
  if(!SMS_SEND_ENDPOINT) return {ok:false, reason:"not_configured"};
  try{
    const res = await fetch(SMS_SEND_ENDPOINT, {
      method:"POST", headers:{"Content-Type":"application/json"},
      body: JSON.stringify({phone, code})
    });
    return {ok: res.ok};
  }catch(e){ return {ok:false, reason:String(e)}; }
}

async function initLiffIfConfigured(){
  if(!LIFF_ID || typeof liff === "undefined"){ state.liffFailed = !!LIFF_ID; return; }
  try{
    await liff.init({ liffId: LIFF_ID });
    state.liffReady = true;
    if(liff.isLoggedIn()){
      const profile = await liff.getProfile();
      const key = "line:"+profile.userId;
      await finishLogin(key, { name: profile.displayName, phone:"-", lineId: profile.userId, picture: profile.pictureUrl });
    }
  }catch(e){ console.error("LIFF init failed", e); state.liffFailed = true; }
}

async function loadAll(){
  try{
    const res = await window.storage.get("reward-coupons", true);
    state.coupons = res && res.value ? JSON.parse(res.value) : DEFAULT_COUPONS.slice();
    if(!res){ await window.storage.set("reward-coupons", JSON.stringify(state.coupons), true); }
  }catch(e){ state.coupons = DEFAULT_COUPONS.slice(); }

  try{
    const mres = await window.storage.get("fy_members", true);
    state.members = mres && mres.value ? JSON.parse(mres.value) : {};
  }catch(e){ state.members = {}; }

  await initLiffIfConfigured(); // may set state.screen = "main" via finishLogin if already logged into LINE

  if(state.screen !== "main"){
    try{
      const sres = await window.storage.get("fy_session", false);
      if(sres && sres.value){
        const {key} = JSON.parse(sres.value);
        if(key && state.members[key]){
          state.sessionKey = key;
          state.customer = state.members[key];
          state.screen = "main";
        }
      }
    }catch(e){ /* no session */ }
  }

  render();
}
async function saveCoupons(){ try{ await window.storage.set("reward-coupons", JSON.stringify(state.coupons), true); }catch(e){ console.error(e); } }
async function saveMembers(){ try{ await window.storage.set("fy_members", JSON.stringify(state.members), true); }catch(e){ console.error(e); } }
async function saveSessionPointer(){ try{ await window.storage.set("fy_session", JSON.stringify({key: state.sessionKey}), false); }catch(e){ console.error(e); } }
async function refreshMembersFromStorage(){
  try{
    const mres = await window.storage.get("fy_members", true);
    state.members = mres && mres.value ? JSON.parse(mres.value) : {};
    if(state.sessionKey && state.members[state.sessionKey]) state.customer = state.members[state.sessionKey];
  }catch(e){ /* keep local copy */ }
}

function render(){
  if(state.screen==="login") return renderLogin();
  if(state.screen==="otp") return renderOtp();
  if(state.screen==="history") return renderHistory();
  if(state.screen==="main") return renderMain();
}

/* ============ LOGIN ============ */
function renderLogin(){
  app.innerHTML = `
    <div class="login-wrap">
      <div class="pagehead" style="background:transparent;border:none;color:#fff;">บัตรสะสมคะแนน</div>
      <div class="login-card">
        <div class="avatar-placeholder"><img src="${LOGO}" alt="โลโก้"></div>
        <h1>เข้าสู่ระบบ/สมัครสมาชิก</h1>
        <p class="sub">เพิ่มเบอร์โทรศัพท์เพื่อสะสมคะแนนหรือ<br>ใช้สิทธิพิเศษสำหรับสมาชิกก่อนใคร</p>
        <input class="tel-input" id="phoneInput" type="tel" placeholder="เบอร์โทรศัพท์" maxlength="10">
        <button class="btn-primary" id="continueBtn" style="margin-top:6px;">ดำเนินการต่อ</button>
        <div class="divider">หรือ</div>
        <button class="btn-line" id="lineBtn"><span class="line-badge">LINE</span> เข้าสู่ระบบด้วย LINE</button>
        ${state.liffReady ? "" : `
        <div class="line-inline" id="lineInlineForm" style="display:none;">
          <input type="text" id="lineIdInput" placeholder="เบอร์โทรศัพท์หรือ LINE ID ที่ลงทะเบียน">
          <button id="lineGoBtn">ต่อ</button>
        </div>
        <div class="setup-note">${state.liffFailed
          ? "เชื่อมต่อ LINE Login ไม่สำเร็จ (ตรวจสอบว่า Endpoint URL ที่ตั้งไว้ใน LINE Developers Console ตรงกับโดเมนที่โฮสต์ไฟล์นี้อยู่ และเปิดผ่าน https) ตอนนี้จึงใช้โหมดกรอกข้อมูลชั่วคราวแทน"
          : "ยังไม่ได้เชื่อมต่อ LINE Login จริง (ต้องตั้งค่า LIFF ID ของร้านก่อน) ตอนนี้จึงใช้โหมดกรอกข้อมูลชั่วคราวแทน"}</div>
        `}
      </div>
    </div>
  `;
  document.getElementById("continueBtn").addEventListener("click", async ()=>{
    const val = document.getElementById("phoneInput").value.trim();
    if(!isPhone(val)){ alert("กรุณากรอกเบอร์โทรศัพท์ให้ถูกต้อง (10 หลัก)"); return; }
    state.phone = val;
    const code = sixDigit();
    state.pendingOtp = { code, expiresAt: Date.now() + 5*60000, phone: val };
    await sendSmsIfConfigured(val, code);
    state.otpError = "";
    state.screen = "otp";
    render();
  });
  document.getElementById("lineBtn").addEventListener("click", ()=>{
    if(state.liffReady && typeof liff !== "undefined"){
      liff.login();
      return;
    }
    document.getElementById("lineInlineForm").style.display = "flex";
    document.getElementById("lineIdInput").focus();
  });
  const lineGoBtn = document.getElementById("lineGoBtn");
  if(lineGoBtn){
    lineGoBtn.addEventListener("click", async ()=>{
      const val = document.getElementById("lineIdInput").value.trim();
      if(!val){ alert("กรุณากรอกเบอร์โทรศัพท์หรือ LINE ID"); return; }
      const key = memberKey(val);
      await finishLogin(key, { name: "เพื่อน LINE", phone: isPhone(val) ? val : "-", lineId: isPhone(val) ? null : val });
    });
  }
}

/* ============ OTP ============ */
function renderOtp(){
  const masked = state.phone.slice(0,3)+"***"+state.phone.slice(6);
  app.innerHTML = `
    <div class="pagehead">บัตรสะสมคะแนน</div>
    <div class="otp-card">
      <h1>ยืนยันเบอร์โทรศัพท์</h1>
      <p class="sub">กรอกรหัส OTP 6 หลัก ที่ส่งไปยัง ${masked}<br>หากยังไม่ได้รับ กรุณากดขอรหัสใหม่</p>
      ${!SMS_SEND_ENDPOINT ? `<div class="dev-note">โหมดทดสอบ: ยังไม่ได้เชื่อมต่อผู้ให้บริการ SMS จริง (ต้องมีเซิร์ฟเวอร์กลางส่งต่อไปยัง Twilio/THSMS ฯลฯ) รหัสสำหรับทดสอบคือ <b>${state.pendingOtp.code}</b></div>` : ""}
      <div class="otp-boxes">${[0,1,2,3,4,5].map(i=>`<input type="text" inputmode="numeric" maxlength="1" data-idx="${i}">`).join("")}</div>
      ${state.otpError ? `<div style="color:var(--red);font-size:0.82rem;margin:-10px 0 18px;">${esc(state.otpError)}</div>` : ""}
      <div class="otp-meta">Ref : ${Math.random().toString(36).slice(2,6).toUpperCase()} &nbsp;|&nbsp; <a id="resendLink">ส่งรหัสอีกครั้ง</a></div>
      <button class="btn-primary" id="verifyBtn">ยืนยัน</button>
    </div>
  `;
  const boxes = Array.from(document.querySelectorAll(".otp-boxes input"));
  boxes.forEach((b,i)=>{
    b.addEventListener("input", ()=>{ b.value = b.value.replace(/[^0-9]/g,""); if(b.value && boxes[i+1]) boxes[i+1].focus(); });
    b.addEventListener("keydown", (e)=>{ if(e.key==="Backspace" && !b.value && boxes[i-1]) boxes[i-1].focus(); });
  });
  boxes[0].focus();
  document.getElementById("resendLink").addEventListener("click", async ()=>{
    const code = sixDigit();
    state.pendingOtp = { code, expiresAt: Date.now() + 5*60000, phone: state.phone };
    await sendSmsIfConfigured(state.phone, code);
    state.otpError = "";
    render();
  });
  document.getElementById("verifyBtn").addEventListener("click", ()=>{
    const typed = boxes.map(b=>b.value).join("");
    if(typed.length < 6){ state.otpError = "กรุณากรอกรหัส OTP ให้ครบ 6 หลัก"; render(); return; }
    if(!state.pendingOtp || Date.now() > state.pendingOtp.expiresAt){ state.otpError = "รหัส OTP หมดอายุ กรุณากดส่งรหัสอีกครั้ง"; render(); return; }
    if(typed !== state.pendingOtp.code){ state.otpError = "รหัส OTP ไม่ถูกต้อง กรุณาลองใหม่อีกครั้ง"; render(); return; }
    state.pendingOtp = null;
    finishLogin(state.phone, {phone: state.phone});
  });
}

async function finishLogin(key, defaults){
  await refreshMembersFromStorage();
  if(!state.members[key]){
    state.members[key] = {
      key, name: defaults.name || ("ลูกค้า "+key.slice(-4)),
      phone: defaults.phone || key, lineId: defaults.lineId || null,
      joined: todayStr(), points: 0, pointsLog: [], claimed: []
    };
    await saveMembers();
  }
  state.customer = state.members[key];
  state.sessionKey = key;
  await saveSessionPointer();
  state.screen = "main";
  render();
}

/* ============ MAIN (with bottom nav) ============ */
function renderMain(){
  let body = "";
  if(state.activeTab==="home") body = homeHtml();
  else if(state.activeTab==="coupons") body = myCouponsHtml();
  else if(state.activeTab==="card") body = cardHtml();
  else if(state.activeTab==="account") body = accountHtml();
  else if(state.activeTab==="admin") body = adminHtml();

  app.innerHTML = `
    <div class="content-scroll">${body}</div>
    <div class="bottom-nav">
      <button data-tab="home" class="${state.activeTab==='home'?'active':''}">${ICONS.home}หน้าหลัก</button>
      <button data-tab="coupons" class="${state.activeTab==='coupons'?'active':''}">${ICONS.ticket}คูปอง</button>
      <button data-tab="card" class="${state.activeTab==='card'?'active':''}">${ICONS.card}บัตรสมาชิก</button>
      <button data-tab="account" class="${state.activeTab==='account'?'active':''}">${ICONS.user}บัญชี</button>
      <button data-tab="admin" class="${state.activeTab==='admin'?'active':''}">${ICONS.gear}ผู้ดูแลระบบ</button>
    </div>
  `;
  document.querySelectorAll(".bottom-nav button").forEach(b=>{
    b.addEventListener("click", ()=>{ state.activeTab = b.dataset.tab; state.adminError=""; render(); });
  });
  wireTabEvents();
}

function homeHtml(){
  const c = state.customer;
  return `
    <div class="home-header">
      <div class="brandrow">
        <div class="brand-avatar"><img src="${LOGO}" alt="โลโก้"></div>
        <div>
          <div class="brandname">${esc(BRAND_NAME)}</div>
          <div class="branch">${esc(BRANCH_NAME)}</div>
        </div>
        <button class="header-iconbtn" id="openHistoryBtn" title="ประวัติคะแนน">${ICONS.history}</button>
      </div>
    </div>
    <div class="member-card">
      <div>
        <div class="name">${esc(c.name)}</div>
        <div class="phone">${esc(c.lineId ? c.lineId : c.phone)}</div>
      </div>
      <div class="pts-badge">
        <div class="num"><span class="pchip">P</span>${c.points}</div>
        <div class="lbl">คะแนน</div>
      </div>
    </div>

    <div class="section-title-row"><h2>คูปองพร้อมแลก</h2></div>
    <div class="coupon-list" id="couponList">
      ${state.coupons.length ? state.coupons.map(cp=>couponCardHtml(cp,false)).join("") : `<div class="empty">ยังไม่มีคูปองให้แลกในขณะนี้</div>`}
    </div>
  `;
}

function couponCardHtml(cp, adminMode){
  const already = state.customer && state.customer.claimed.some(x=>x.couponId===cp.id);
  const canAfford = state.customer && state.customer.points >= cp.cost;
  return `
    <div class="coupon-card">
      <div class="coupon-img" style="${cp.image?'':'background:linear-gradient(135deg,#BFE0FA,#8FC8F2);'}">
        ${cp.image ? `<img src="${cp.image}" alt="">` : `<span style="color:#fff;font-size:1.6rem;font-weight:800;">P${cp.cost}</span>`}
      </div>
      <div class="coupon-body">
        <div class="ttl">${esc(cp.title)}</div>
        <div class="desc">${esc(cp.desc)}</div>
        <div class="expiry">ใช้ได้จนถึง ${fmtDate(cp.expiry)}</div>
        <div class="bottomrow">
          <div class="cost"><span class="pchip">P</span>${cp.cost} คะแนน</div>
          <div class="rowicons">
            ${adminMode ? `
              <button class="icobtn" data-edit="${cp.id}" title="แก้ไข">${ICONS.edit}</button>
              <button class="icobtn danger" data-del="${cp.id}" title="ลบ">${ICONS.trash}</button>
            ` : `<button class="redeembtn" data-redeem="${cp.id}" ${(already||!canAfford)?'disabled':''}>${already?'แลกแล้ว':'แลก'}</button>`}
          </div>
        </div>
      </div>
    </div>
  `;
}

function myCouponsHtml(){
  const items = state.customer.claimed.map(cl=>{
    const cp = state.coupons.find(c=>c.id===cl.couponId);
    if(!cp) return "";
    return `
      <div class="coupon-card" ${cl.used ? "" : `data-showqr="${cl.token}" style="cursor:pointer;"`}>
        <div class="coupon-img" style="${cp.image?'':'background:linear-gradient(135deg,#C9E9D2,#8FD1A6);'}">
          ${cp.image ? `<img src="${cp.image}" alt="">` : `<span style="color:#fff;font-size:1.6rem;font-weight:800;">${cl.used?'✓':'P'}</span>`}
        </div>
        <div class="coupon-body">
          <div class="ttl">${esc(cp.title)}</div>
          <div class="desc">${esc(cp.desc)}</div>
          <div class="expiry">แลกเมื่อ ${fmtDate(cl.date)}</div>
          <div class="bottomrow">
            ${cl.used
              ? `<span style="color:var(--sub);font-size:0.8rem;">ใช้สิทธิ์แล้ว${cl.usedAt?(' · '+fmtDateTime(cl.usedAt)):''}</span>`
              : `<span style="color:var(--blue);font-size:0.8rem;font-weight:700;">แตะเพื่อแสดง QR ใช้สิทธิ์ ›</span>`}
          </div>
        </div>
      </div>
    `;
  }).join("");
  return `
    <div class="pagehead">คูปองของฉัน</div>
    <div class="coupon-list" style="padding-top:18px;">${items || `<div class="empty">ยังไม่มีคูปองที่แลกไว้</div>`}</div>
  `;
}

function openCouponUseQr(token){
  const cl = state.customer.claimed.find(c=>c.token===token);
  if(!cl) return;
  const cp = state.coupons.find(c=>c.id===cl.couponId);
  const backdrop = document.createElement("div");
  backdrop.className = "sheet-backdrop";
  backdrop.innerHTML = `
    <div class="sheet" style="text-align:center;">
      <h3>${esc(cp ? cp.title : "คูปอง")}</h3>
      <div class="qr-box" id="useQrBox" style="margin:10px auto 14px;"></div>
      <div id="useStatusText" style="font-size:0.88rem;color:var(--ink);margin-bottom:6px;">ให้พนักงานสแกน QR นี้ที่เคาน์เตอร์เพื่อใช้สิทธิ์</div>
      <div style="font-size:0.76rem;color:var(--sub);">หน้านี้จะอัปเดตสถานะให้อัตโนมัติเมื่อพนักงานสแกนสำเร็จ</div>
      <div class="sheet-actions"><button class="cancel" id="closeUseQr" style="width:100%;">ปิด</button></div>
    </div>
  `;
  document.body.appendChild(backdrop);
  backdrop.addEventListener("click", (e)=>{ if(e.target===backdrop) stopAndClose(); });
  document.getElementById("closeUseQr").addEventListener("click", stopAndClose);

  drawQrInto("useQrBox", QR_USE_PREFIX + state.customer.key + "|" + token);

  const poll = setInterval(async ()=>{
    await refreshMembersFromStorage();
    const fresh = state.customer.claimed.find(c=>c.token===token);
    if(fresh && fresh.used){
      clearInterval(poll);
      document.getElementById("useQrBox").innerHTML = "";
      document.getElementById("useStatusText").innerHTML = "✅ ใช้สิทธิ์แล้ว! พนักงานสแกนคูปองนี้เรียบร้อย";
      setTimeout(()=>{ stopAndClose(); render(); }, 1800);
    }
  }, 2000);

  function stopAndClose(){ clearInterval(poll); if(document.body.contains(backdrop)) document.body.removeChild(backdrop); }
}

function cardHtml(){
  const c = state.customer;
  return `
    <div class="pagehead">บัตรสมาชิก</div>
    <div class="qr-wrap">
      <div class="qr-card">
        <div class="qr-inner">
          <div class="qr-avatar"><img src="${LOGO}" alt="โลโก้"></div>
          <div class="qr-name">${esc(c.name)}</div>
          <div class="qr-box" id="qrBox"></div>
          <div class="qr-caption">กรุณาแสดง QR นี้ให้พนักงานเพื่อสะสม/แลกคะแนน</div>
          <div class="qr-key">รหัสสมาชิก: ${esc(c.key)}</div>
        </div>
      </div>
    </div>
  `;
}

function accountHtml(){
  const c = state.customer;
  return `
    <div class="pagehead">บัญชีของฉัน</div>
    <div class="acct-wrap">
      <div class="acct-row"><span>ชื่อ</span><span>${esc(c.name)}</span></div>
      <div class="acct-row"><span>เบอร์โทรศัพท์</span><span>${esc(c.phone)}</span></div>
      ${c.lineId ? `<div class="acct-row"><span>LINE ID</span><span>${esc(c.lineId)}</span></div>` : ""}
      <div class="acct-row"><span>สมัครเมื่อ</span><span>${fmtDate(c.joined)}</span></div>
      <div class="acct-row"><span>คะแนนคงเหลือ</span><span>${c.points} คะแนน</span></div>
      <div class="acct-actions"><button class="btn-primary" id="logoutBtn" style="background:#F1F2F4;color:var(--red);">ออกจากระบบ</button></div>
    </div>
  `;
}

/* ============ POINTS HISTORY ============ */
function renderHistory(){
  const c = state.customer;
  const log = (c.pointsLog||[]).slice().reverse();
  const filtered = log.filter(x => state.historyFilter==="all" ? true : x.type===state.historyFilter);
  app.innerHTML = `
    <div class="pagehead"><button class="back" id="histBack">${ICONS.back}</button>ประวัติคะแนน</div>
    <div class="hist-headcard">
      <div class="hist-card">
        <div class="lbl">คะแนนของฉัน</div>
        <div class="num"><span class="pchip">P</span>${c.points}</div>
      </div>
    </div>
    <div class="hist-tabs">
      <button data-f="all" class="${state.historyFilter==='all'?'active':''}">ทั้งหมด</button>
      <button data-f="earn" class="${state.historyFilter==='earn'?'active':''}">คะแนนที่ได้รับ</button>
      <button data-f="use" class="${state.historyFilter==='use'?'active':''}">คะแนนที่ใช้</button>
    </div>
    <div class="hist-list">
      ${filtered.length ? filtered.map(it=>`
        <div class="hist-item">
          <div>
            <div class="note">${esc(it.note)}</div>
            <div class="date">${fmtDateTime(it.date)}</div>
          </div>
          <div class="amt ${it.type}">${it.type==='earn'?'+':'-'}${it.amount}</div>
        </div>
      `).join("") : `
        <div class="empty">${ICONS.searchdoc}<div>ไม่พบข้อมูลประวัติคะแนน</div></div>
      `}
    </div>
  `;
  document.getElementById("histBack").addEventListener("click", ()=>{ state.screen="main"; render(); });
  document.querySelectorAll(".hist-tabs button").forEach(b=>{
    b.addEventListener("click", ()=>{ state.historyFilter=b.dataset.f; render(); });
  });
}

/* ============ ADMIN ============ */
function adminHtml(){
  if(!state.isAdmin){
    return `
      <div class="pagehead">ผู้ดูแลระบบ</div>
      <div class="admin-lock">
        <div class="lockicon">${ICONS.lock}</div>
        <h1>สำหรับผู้ดูแลระบบเท่านั้น</h1>
        <p>กรอกรหัสผ่านเพื่อจัดการคูปองและสแกน QR สมาชิก</p>
        <div class="field" style="text-align:left;"><input type="password" id="adminPass" placeholder="รหัสผ่านผู้ดูแลระบบ"></div>
        ${state.adminError ? `<div style="color:var(--red);font-size:0.82rem;margin-bottom:14px;">${esc(state.adminError)}</div>` : ""}
        <button class="btn-primary" id="adminLoginBtn">เข้าสู่ระบบผู้ดูแลระบบ</button>
      </div>
    `;
  }
  return `
    <div class="pagehead">ผู้ดูแลระบบ</div>
    <div class="admin-panel">
      <span class="admin-badge">${ICONS.gear} โหมดผู้ดูแลระบบ</span>

      <div class="toolbox">
        <h3>สแกน QR สมาชิก</h3>
        <p style="font-size:0.8rem;color:var(--sub);margin:0 0 10px;">สแกน QR จากบัตรสมาชิกของลูกค้าเพื่อเพิ่มคะแนนหรือแลกคูปองให้ทันที</p>
        <div class="toolrow"><button class="primary" id="scanQrBtn">เปิดกล้องสแกน QR</button></div>
      </div>

      <div class="toolbox">
        <h3>เครื่องมือทดสอบระบบ</h3>
        <div class="toolrow">
          <button id="addTestPtsBtn">+10 คะแนนให้บัญชีที่ล็อกอินอยู่</button>
          <button id="adminLogoutBtn">ออกจากโหมดผู้ดูแลระบบ</button>
        </div>
      </div>

      <div class="section-title-row" style="padding:0 0 12px;">
        <h2>จัดการคูปอง</h2>
        <button class="addbtn" id="addCouponBtn">+ เพิ่มคูปอง</button>
      </div>
      <div class="coupon-list" id="adminCouponList" style="padding:0;">
        ${state.coupons.length ? state.coupons.map(cp=>couponCardHtml(cp,true)).join("") : `<div class="empty">ยังไม่มีคูปอง กด “เพิ่มคูปอง” เพื่อเริ่มสร้างรายการ</div>`}
      </div>
    </div>
  `;
}

/* ============ event wiring per tab ============ */
function wireTabEvents(){
  if(state.activeTab==="home"){
    const hb = document.getElementById("openHistoryBtn");
    if(hb) hb.addEventListener("click", ()=>{ state.screen="history"; state.historyFilter="all"; render(); });
    document.querySelectorAll("[data-redeem]").forEach(b=>{
      b.addEventListener("click", async ()=>{
        const cp = state.coupons.find(c=>c.id===b.dataset.redeem);
        if(!cp) return;
        if(state.customer.points < cp.cost){ alert("คะแนนไม่เพียงพอ"); return; }
        state.customer.points -= cp.cost;
        state.customer.claimed.push({couponId:cp.id, date: todayStr(), token: uid(), used:false, usedAt:null});
        state.customer.pointsLog = state.customer.pointsLog || [];
        state.customer.pointsLog.push({type:"use", amount:cp.cost, date:new Date().toISOString(), note:"แลกคูปอง: "+cp.title});
        await saveMembers();
        render();
      });
    });
  }
  if(state.activeTab==="card"){ drawRealQr(); }
  if(state.activeTab==="coupons"){
    document.querySelectorAll("[data-showqr]").forEach(el=>{
      el.addEventListener("click", ()=>openCouponUseQr(el.dataset.showqr));
    });
  }
  if(state.activeTab==="account"){
    document.getElementById("logoutBtn").addEventListener("click", async ()=>{
      if(confirm("ต้องการออกจากระบบหรือไม่?")){
        try{ await window.storage.delete("fy_session", false); }catch(e){}
        state.customer = null; state.sessionKey=null; state.screen = "login"; state.activeTab="home";
        render();
      }
    });
  }
  if(state.activeTab==="admin"){
    if(!state.isAdmin){
      const passInput = document.getElementById("adminPass");
      const doLogin = ()=>{
        if(passInput.value === ADMIN_PASSWORD){ state.isAdmin = true; state.adminError=""; render(); }
        else{ state.adminError = "รหัสผ่านไม่ถูกต้อง กรุณาลองใหม่อีกครั้ง"; render(); }
      };
      document.getElementById("adminLoginBtn").addEventListener("click", doLogin);
      passInput.addEventListener("keydown", (e)=>{ if(e.key==="Enter") doLogin(); });
      passInput.focus();
    }else{
      document.getElementById("scanQrBtn").addEventListener("click", openScanner);
      document.getElementById("addTestPtsBtn").addEventListener("click", async ()=>{
        if(!state.customer){ alert("ยังไม่มีลูกค้าล็อกอินอยู่ในเซสชันนี้"); return; }
        state.customer.points += 10;
        state.customer.pointsLog = state.customer.pointsLog || [];
        state.customer.pointsLog.push({type:"earn", amount:10, date:new Date().toISOString(), note:"ทดสอบระบบ"});
        await saveMembers();
        render();
      });
      document.getElementById("adminLogoutBtn").addEventListener("click", ()=>{ state.isAdmin = false; state.activeTab = "home"; render(); });
      document.getElementById("addCouponBtn").addEventListener("click", ()=>openCouponForm(null));
      document.querySelectorAll("[data-edit]").forEach(b=>{
        b.addEventListener("click", ()=>openCouponForm(state.coupons.find(c=>c.id===b.dataset.edit)));
      });
      document.querySelectorAll("[data-del]").forEach(b=>{
        b.addEventListener("click", async ()=>{
          if(confirm("ต้องการลบคูปองนี้หรือไม่?")){
            state.coupons = state.coupons.filter(c=>c.id!==b.dataset.del);
            await saveCoupons();
            render();
          }
        });
      });
    }
  }
}

/* ============ coupon add/edit sheet (admin only) ============ */
function openCouponForm(existing){
  const isNew = !existing;
  const data = existing || {id:null, image:null, title:"", desc:"", cost:10, expiry: addDays(todayStr(),30)};
  const backdrop = document.createElement("div");
  backdrop.className = "sheet-backdrop";
  backdrop.innerHTML = `
    <div class="sheet">
      <h3>${isNew ? "เพิ่มคูปอง" : "แก้ไขคูปอง"}</h3>
      <div class="field"><label>รูปภาพ</label>
        <div class="imgpick">
          <div class="preview" id="imgPreview">${data.image?`<img src="${data.image}" style="width:100%;height:100%;object-fit:cover;border-radius:10px;">`:"ไม่มีรูป"}</div>
          <label class="upl">เลือกรูปภาพ<input type="file" accept="image/*" id="imgFile" style="display:none;"></label>
        </div>
      </div>
      <div class="field"><label>ชื่อคูปอง</label><input type="text" id="fTitle" value="${esc(data.title)}" placeholder="เช่น แลกฟรีส่วนลด 10 บาท"></div>
      <div class="field"><label>รายละเอียด</label><textarea id="fDesc" placeholder="เงื่อนไขการใช้คูปอง">${esc(data.desc)}</textarea></div>
      <div class="field"><label>คะแนนที่ใช้แลก</label><input type="number" id="fCost" min="1" value="${data.cost}"></div>
      <div class="field"><label>วันหมดอายุ</label><input type="date" id="fExpiry" value="${data.expiry}"></div>
      <div class="sheet-actions"><button class="cancel" id="cancelSheet">ยกเลิก</button><button class="save" id="saveSheet">บันทึก</button></div>
    </div>
  `;
  document.body.appendChild(backdrop);

  let imageData = data.image;
  document.getElementById("imgFile").addEventListener("change", (e)=>{
    const file = e.target.files[0];
    if(!file) return;
    const reader = new FileReader();
    reader.onload = ()=>{
      imageData = reader.result;
      document.getElementById("imgPreview").innerHTML = `<img src="${imageData}" style="width:100%;height:100%;object-fit:cover;border-radius:10px;">`;
    };
    reader.readAsDataURL(file);
  });

  backdrop.addEventListener("click", (e)=>{ if(e.target===backdrop) document.body.removeChild(backdrop); });
  document.getElementById("cancelSheet").addEventListener("click", ()=>document.body.removeChild(backdrop));
  document.getElementById("saveSheet").addEventListener("click", async ()=>{
    const title = document.getElementById("fTitle").value.trim();
    const cost = parseInt(document.getElementById("fCost").value,10);
    if(!title || !cost || cost<=0){ alert("กรุณากรอกชื่อคูปองและคะแนนให้ถูกต้อง"); return; }
    const payload = { id: data.id || uid(), image: imageData, title, desc: document.getElementById("fDesc").value.trim(), cost, expiry: document.getElementById("fExpiry").value || addDays(todayStr(),30) };
    if(isNew) state.coupons.push(payload); else Object.assign(existing, payload);
    await saveCoupons();
    document.body.removeChild(backdrop);
    render();
  });
}

/* ============ real QR generation ============ */
function drawQrInto(elId, text, attempt){
  attempt = attempt || 0;
  const box = document.getElementById(elId);
  if(!box) return;
  if(typeof QRCode === "undefined"){
    if(attempt < 10){ setTimeout(()=>drawQrInto(elId, text, attempt+1), 300); return; }
    box.innerHTML = `<div class="empty">ไม่สามารถโหลดตัวสร้าง QR ได้ (ต้องมีอินเทอร์เน็ต)</div>`;
    return;
  }
  box.innerHTML = "";
  new QRCode(box, {
    text: text, width: 230, height: 230,
    colorDark: "#161A1F", colorLight: "#ffffff",
    correctLevel: QRCode.CorrectLevel.H
  });
  const center = document.createElement("div");
  center.className = "qr-center";
  center.innerHTML = ICONS.star;
  box.appendChild(center);
}
function drawRealQr(){
  if(!document.getElementById("qrBox") || !state.customer) return;
  drawQrInto("qrBox", QR_PREFIX + state.customer.key);
}

/* ============ admin camera QR scanner ============ */
function openScanner(){
  if(typeof jsQR === "undefined"){ alert("ไม่สามารถโหลดตัวอ่าน QR ได้ (ต้องมีอินเทอร์เน็ต)"); return; }
  const overlay = document.createElement("div");
  overlay.className = "scan-overlay";
  overlay.innerHTML = `
    <div class="scan-box">
      <div class="scan-head"><span>สแกน QR สมาชิก</span><button id="closeScanBtn">${ICONS.close}</button></div>
      <video id="scanVideo" playsinline muted style="width:100%;border-radius:10px;background:#000;display:block;"></video>
      <canvas id="scanCanvas" style="display:none;"></canvas>
      <div class="scan-note">ต้องอนุญาตให้เว็บไซต์ใช้กล้อง และเปิดผ่าน https หรือ localhost กล้องจึงจะทำงานได้</div>
      <div id="scanResultArea"></div>
    </div>
  `;
  document.body.appendChild(overlay);

  document.getElementById("closeScanBtn").addEventListener("click", closeScanner);

  const video = document.getElementById("scanVideo");
  const canvas = document.getElementById("scanCanvas");
  const ctx = canvas.getContext("2d");

  startCamera();

  async function startCamera(){
    const resultArea = document.getElementById("scanResultArea");
    if(!window.isSecureContext){
      resultArea.innerHTML = `<div style="color:var(--red);font-size:0.85rem;margin-top:12px;">เบราว์เซอร์บล็อกการใช้กล้องเพราะหน้านี้ไม่ได้เปิดผ่าน HTTPS หรือ localhost กรุณาอัปโหลดไฟล์นี้ขึ้นโฮสติ้งที่เป็น https แล้วเปิดผ่านลิงก์นั้นแทนการเปิดไฟล์ตรงๆ</div>`;
      return;
    }
    if(!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia){
      resultArea.innerHTML = `<div style="color:var(--red);font-size:0.85rem;margin-top:12px;">เบราว์เซอร์นี้ไม่รองรับการเข้าถึงกล้อง (getUserMedia) กรุณาลองเปิดด้วย Chrome หรือ Safari เวอร์ชันล่าสุด</div>`;
      return;
    }
    try{
      const stream = await navigator.mediaDevices.getUserMedia({video:{facingMode:{ideal:"environment"}}, audio:false});
      state.scanStream = stream;
      video.srcObject = stream;
      video.setAttribute("playsinline", true);
      await video.play();
      state.scanRAF = requestAnimationFrame(tick);
    }catch(err){
      resultArea.innerHTML = `<div style="color:var(--red);font-size:0.85rem;margin-top:12px;">ไม่สามารถเปิดกล้องได้: ${esc(err && err.message ? err.message : String(err))}<br>กรุณากดอนุญาตให้เว็บไซต์ใช้กล้องเมื่อเบราว์เซอร์ถาม แล้วลองใหม่</div>`;
    }
  }

  function tick(){
    if(!document.getElementById("scanVideo")) return; // overlay closed
    if(video.readyState === video.HAVE_ENOUGH_DATA){
      canvas.width = video.videoWidth; canvas.height = video.videoHeight;
      ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
      const imgData = ctx.getImageData(0,0,canvas.width,canvas.height);
      const code = jsQR(imgData.data, imgData.width, imgData.height);
      const area = document.getElementById("scanResultArea");
      if(code && code.data){
        if(code.data.indexOf(QR_USE_PREFIX)===0){
          handleScanUse(code.data.slice(QR_USE_PREFIX.length));
          return;
        }else if(code.data.indexOf(QR_PREFIX)===0){
          handleScanResult(code.data.slice(QR_PREFIX.length));
          return;
        }else if(area && !area.querySelector(".found-card")){
          area.innerHTML = `<div style="color:var(--red);font-size:0.82rem;margin-top:12px;">พบ QR แต่ไม่ใช่ QR ของร้าน Fresh Yogurt — ระบบรับสแกนเฉพาะ QR ของร้านนี้เท่านั้น</div>`;
        }
      }
    }
    state.scanRAF = requestAnimationFrame(tick);
  }
}

function closeScanner(){
  if(state.scanRAF){ cancelAnimationFrame(state.scanRAF); state.scanRAF = null; }
  if(state.scanStream){ state.scanStream.getTracks().forEach(t=>t.stop()); state.scanStream = null; }
  const overlay = document.querySelector(".scan-overlay");
  if(overlay) overlay.remove();
}

async function handleScanResult(key){
  await refreshMembersFromStorage();
  const member = state.members[key];
  const area = document.getElementById("scanResultArea");
  if(!member){
    if(area) area.innerHTML = `<div style="color:var(--red);font-size:0.85rem;margin-top:12px;">เป็น QR ของร้านนี้จริง แต่ไม่พบข้อมูลสมาชิกรายนี้ในระบบ (อาจยังไม่เคยลงทะเบียน)</div>`;
    return;
  }
  if(state.scanRAF){ cancelAnimationFrame(state.scanRAF); state.scanRAF = null; }
  const affordable = state.coupons.filter(c=>member.points>=c.cost);
  area.innerHTML = `
    <div class="found-card">
      <div class="fname">${esc(member.name)}</div>
      <div class="fmeta">${esc(member.phone)}${member.lineId?(" · LINE: "+esc(member.lineId)):""} · แต้มคงเหลือ ${member.points} คะแนน</div>
      <div class="found-row">
        <input type="number" id="addPtsInput" placeholder="จำนวนคะแนนที่จะเพิ่ม" min="1">
        <button id="addPtsConfirm">เพิ่มคะแนน</button>
      </div>
      <div class="found-row">
        <select id="redeemSelect">
          <option value="">— เลือกคูปองเพื่อแลกให้ลูกค้า —</option>
          ${affordable.map(c=>`<option value="${c.id}">${esc(c.title)} (${c.cost} คะแนน)</option>`).join("")}
        </select>
        <button id="redeemConfirm">แลกให้</button>
      </div>
      <button id="scanAgainBtn" style="background:none;border:1px solid var(--line);color:var(--sub);border-radius:8px;padding:8px 12px;font-size:0.8rem;width:100%;">สแกนสมาชิกคนถัดไป</button>
    </div>
  `;
  document.getElementById("addPtsConfirm").addEventListener("click", async ()=>{
    const amt = parseInt(document.getElementById("addPtsInput").value,10);
    if(!amt || amt<=0){ alert("กรุณาระบุจำนวนคะแนนให้ถูกต้อง"); return; }
    member.points += amt;
    member.pointsLog = member.pointsLog || [];
    member.pointsLog.push({type:"earn", amount:amt, date:new Date().toISOString(), note:"สะสมคะแนนโดยพนักงาน"});
    await saveMembers();
    alert("เพิ่มคะแนนให้ "+member.name+" เรียบร้อย");
    closeScanner();
  });
  document.getElementById("redeemConfirm").addEventListener("click", async ()=>{
    const cid = document.getElementById("redeemSelect").value;
    if(!cid){ alert("กรุณาเลือกคูปอง"); return; }
    const cp = state.coupons.find(c=>c.id===cid);
    if(!cp || member.points < cp.cost){ alert("คะแนนของลูกค้าไม่เพียงพอ"); return; }
    member.points -= cp.cost;
    member.claimed = member.claimed || [];
    member.claimed.push({couponId:cp.id, date: todayStr(), token: uid(), used:true, usedAt: new Date().toISOString()});
    member.pointsLog = member.pointsLog || [];
    member.pointsLog.push({type:"use", amount:cp.cost, date:new Date().toISOString(), note:"แลกคูปอง: "+cp.title+" (โดยพนักงาน)"});
    await saveMembers();
    alert("แลกคูปองให้ "+member.name+" เรียบร้อย");
    closeScanner();
  });
  document.getElementById("scanAgainBtn").addEventListener("click", ()=>{ closeScanner(); openScanner(); });
}

async function handleScanUse(rest){
  const idx = rest.indexOf("|");
  const mKey = idx>=0 ? rest.slice(0,idx) : rest;
  const token = idx>=0 ? rest.slice(idx+1) : "";
  await refreshMembersFromStorage();
  const member = state.members[mKey];
  const area = document.getElementById("scanResultArea");
  if(!member){
    if(area) area.innerHTML = `<div style="color:var(--red);font-size:0.85rem;margin-top:12px;">ไม่พบข้อมูลสมาชิกของคูปองนี้</div>`;
    return;
  }
  const claim = (member.claimed||[]).find(c=>c.token===token);
  const cp = claim ? state.coupons.find(c=>c.id===claim.couponId) : null;
  if(state.scanRAF){ cancelAnimationFrame(state.scanRAF); state.scanRAF = null; }
  if(!claim || !cp){
    area.innerHTML = `<div style="color:var(--red);font-size:0.85rem;margin-top:12px;">ไม่พบคูปองนี้ในระบบ</div>`;
    return;
  }
  if(claim.used){
    area.innerHTML = `<div class="found-card"><div class="fname">คูปองนี้ถูกใช้ไปแล้ว</div><div class="fmeta">${esc(cp.title)} · ${esc(member.name)} · ใช้เมื่อ ${fmtDateTime(claim.usedAt)}</div>
      <button id="scanAgainBtn2" style="background:none;border:1px solid var(--line);color:var(--sub);border-radius:8px;padding:8px 12px;font-size:0.8rem;width:100%;margin-top:6px;">สแกนต่อ</button></div>`;
    document.getElementById("scanAgainBtn2").addEventListener("click", ()=>{ closeScanner(); openScanner(); });
    return;
  }
  area.innerHTML = `
    <div class="found-card">
      <div class="fname">${esc(cp.title)}</div>
      <div class="fmeta">ลูกค้า: ${esc(member.name)} (${esc(member.phone)})</div>
      <button id="confirmUseBtn" style="width:100%;background:var(--blue);color:#fff;border:none;border-radius:8px;padding:11px;font-size:0.9rem;font-weight:700;">ยืนยันใช้สิทธิ์คูปองนี้</button>
    </div>
  `;
  document.getElementById("confirmUseBtn").addEventListener("click", async ()=>{
    claim.used = true;
    claim.usedAt = new Date().toISOString();
    await saveMembers();
    area.innerHTML = `<div class="found-card"><div class="fname">✅ ใช้สิทธิ์สำเร็จ</div><div class="fmeta">${esc(cp.title)} · ${esc(member.name)}</div></div>`;
    setTimeout(closeScanner, 1500);
  });
}

loadAll();
})();
</script>
</body>
</html>
