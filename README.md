<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#0B4F6C">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="PedeFácil">
<title>PedeFácil — Peça antes, curta mais</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root {
  --ocean: #0B4F6C; --wave: #1A7A9A; --sky: #22B5D4;
  --cream: #F5E6C8; --sand: #E8D5A3; --yellow: #F5C518;
  --coral: #FF6B4A; --coral-light: #FF8B6E; --lime: #C8E832;
  --white: #FFFFFF; --dark: #0D2B3E; --mid: #4A6A7C;
  --light: #D4EBF5; --success: #2ECC71; --danger: #E74C3C;
  --radius: 20px; --radius-sm: 12px;
}
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
body { font-family:'DM Sans',sans-serif; background:var(--cream); min-height:100vh; overflow-x:hidden; max-width:480px; margin:0 auto; position:relative; }
.screen { display:none; min-height:100vh; flex-direction:column; animation:fadeUp 0.3s ease; }
.screen.active { display:flex; }
@keyframes fadeUp { from{opacity:0;transform:translateY(16px)} to{opacity:1;transform:translateY(0)} }

/* BUTTONS */
.btn { border:none; border-radius:var(--radius); padding:15px 24px; font-family:'Syne',sans-serif; font-weight:700; font-size:15px; cursor:pointer; width:100%; transition:all 0.2s; }
.btn-primary { background:var(--coral); color:var(--white); box-shadow:0 4px 16px rgba(255,107,74,0.35); }
.btn-primary:hover { background:var(--coral-light); transform:translateY(-2px); }
.btn-ocean { background:var(--ocean); color:var(--white); }
.btn-ocean:hover { background:var(--wave); }
.btn-outline { background:transparent; color:var(--ocean); border:2px solid var(--ocean); }
.btn-white { background:var(--white); color:var(--ocean); }
.btn-success { background:var(--success); color:var(--white); }
.btn-sm { padding:10px 18px; font-size:13px; border-radius:var(--radius-sm); }

/* INPUTS */
.input-group { margin-bottom:14px; }
.input-group label { font-size:12px; font-weight:600; color:var(--mid); letter-spacing:0.5px; text-transform:uppercase; display:block; margin-bottom:6px; }
.input-group input, .input-group select, .input-group textarea {
  width:100%; padding:13px 16px; border-radius:var(--radius-sm);
  border:2px solid var(--sand); background:var(--white);
  font-family:'DM Sans',sans-serif; font-size:15px; color:var(--dark);
  transition:border-color 0.2s; outline:none;
}
.input-group input:focus, .input-group select:focus { border-color:var(--ocean); }
.input-group textarea { min-height:80px; resize:none; }

/* TAGS */
.tag { display:inline-block; padding:4px 10px; border-radius:30px; font-size:11px; font-weight:700; letter-spacing:0.3px; }
.tag-yellow { background:var(--yellow); color:var(--dark); }
.tag-ocean { background:var(--ocean); color:var(--white); }
.tag-coral { background:var(--coral); color:var(--white); }
.tag-success { background:var(--success); color:var(--white); }
.tag-lime { background:var(--lime); color:var(--dark); }

/* TOP BAR */
.topbar { display:flex; align-items:center; justify-content:space-between; padding:16px 20px 10px; }
.topbar .logo { font-family:'Syne',sans-serif; font-weight:800; font-size:22px; color:var(--ocean); }
.topbar .logo span { color:var(--coral); }
.back-btn { width:40px; height:40px; border-radius:50%; background:var(--white); border:none; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:18px; box-shadow:0 2px 8px rgba(0,0,0,0.1); }

/* HERO */
.hero { padding:20px 20px 50px; background:linear-gradient(160deg,var(--ocean),var(--wave)); position:relative; }
.hero::after { content:''; position:absolute; bottom:-2px; left:0; right:0; height:45px; background:var(--cream); clip-path:ellipse(65% 100% at 50% 100%); }
.hero h2 { font-family:'Syne',sans-serif; font-size:22px; color:var(--white); font-weight:800; margin-top:8px; }
.hero p { color:rgba(255,255,255,0.7); font-size:13px; margin-top:4px; }

/* CARDS */
.card { background:var(--white); border-radius:var(--radius); padding:16px; box-shadow:0 2px 12px rgba(0,0,0,0.07); margin-bottom:12px; }
.card-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:10px; }
.card-title { font-family:'Syne',sans-serif; font-weight:700; font-size:15px; color:var(--dark); }

/* BOTTOM NAV */
.bottom-nav { display:flex; background:var(--white); border-top:1px solid var(--sand); padding:8px 0 4px; position:fixed; bottom:0; left:50%; transform:translateX(-50%); width:100%; max-width:480px; z-index:100; }
.nav-btn { flex:1; border:none; background:transparent; cursor:pointer; font-size:11px; font-weight:600; color:var(--mid); display:flex; flex-direction:column; align-items:center; gap:3px; padding:4px; transition:color 0.15s; }
.nav-btn .ni { font-size:22px; }
.nav-btn.active { color:var(--ocean); }

/* MODAL */
.modal { display:none; position:fixed; inset:0; background:rgba(0,0,0,0.5); z-index:200; align-items:flex-end; }
.modal.open { display:flex; }
.modal-box { background:var(--white); border-radius:30px 30px 0 0; padding:24px; width:100%; animation:slideUp 0.3s ease; max-height:85vh; overflow-y:auto; }
@keyframes slideUp { from{transform:translateY(100%)} to{transform:translateY(0)} }
.modal-close { float:right; background:var(--sand); border:none; border-radius:50%; width:32px; height:32px; cursor:pointer; font-size:16px; }
.modal-title { font-family:'Syne',sans-serif; font-weight:800; font-size:20px; margin-bottom:16px; color:var(--dark); }

/* CART BAR */
.cart-bar { position:fixed; bottom:68px; left:50%; transform:translateX(-50%) translateY(120px); width:calc(100% - 40px); max-width:440px; background:var(--ocean); border-radius:var(--radius); padding:14px 18px; display:flex; align-items:center; justify-content:space-between; box-shadow:0 8px 30px rgba(11,79,108,0.4); cursor:pointer; transition:all 0.3s; z-index:99; }
.cart-bar.visible { transform:translateX(-50%) translateY(0); }
.cart-badge { background:var(--coral); color:var(--white); border-radius:50%; width:26px; height:26px; display:flex; align-items:center; justify-content:center; font-weight:700; font-size:13px; }
.cart-total { font-family:'Syne',sans-serif; font-weight:800; font-size:16px; color:var(--lime); }

/* ── SPLASH ── */
#s-splash { background:linear-gradient(160deg,var(--ocean),var(--wave)); align-items:center; justify-content:center; text-align:center; padding:40px 30px; position:relative; overflow:hidden; }
#s-splash::before { content:''; position:absolute; bottom:0; left:0; right:0; height:220px; background:var(--cream); clip-path:ellipse(60% 100% at 50% 100%); }
.splash-content { position:relative; z-index:1; }
.splash-icon { font-size:80px; animation:bob 3s ease-in-out infinite; }
@keyframes bob { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-10px)} }
.splash-logo { font-family:'Syne',sans-serif; font-weight:800; font-size:44px; color:var(--white); letter-spacing:-1px; }
.splash-logo span { color:var(--yellow); }
.splash-sub { color:rgba(255,255,255,0.7); font-size:15px; margin:8px 0 36px; }
.splash-features { display:flex; gap:10px; justify-content:center; margin-bottom:36px; }
.splash-feat { background:rgba(255,255,255,0.15); backdrop-filter:blur(10px); border:1px solid rgba(255,255,255,0.2); border-radius:14px; padding:14px 12px; text-align:center; flex:1; }
.splash-feat .fi { font-size:24px; margin-bottom:5px; }
.splash-feat .fl { font-size:11px; color:rgba(255,255,255,0.85); font-weight:500; line-height:1.3; }
.splash-btns { display:flex; flex-direction:column; gap:10px; width:100%; max-width:320px; margin:0 auto; }

/* ── LOGIN ── */
#s-login { background:var(--cream); }
.login-header { padding:50px 30px 40px; text-align:center; background:linear-gradient(160deg,var(--ocean),var(--wave)); position:relative; }
.login-header::after { content:''; position:absolute; bottom:-30px; left:0; right:0; height:60px; background:var(--cream); clip-path:ellipse(60% 100% at 50% 100%); }
.login-header h2 { font-family:'Syne',sans-serif; font-weight:800; font-size:26px; color:var(--white); }
.login-header p { color:rgba(255,255,255,0.7); margin-top:6px; font-size:14px; }
.login-body { padding:50px 24px 30px; flex:1; }
.login-divider { text-align:center; color:var(--mid); font-size:13px; margin:14px 0; position:relative; }
.login-divider::before,.login-divider::after { content:''; position:absolute; top:50%; width:38%; height:1px; background:var(--sand); }
.login-divider::before{left:0} .login-divider::after{right:0}
.login-tabs { display:flex; gap:8px; margin-bottom:20px; }
.login-tab { flex:1; padding:10px; border-radius:var(--radius-sm); border:2px solid var(--sand); background:var(--white); font-family:'Syne',sans-serif; font-weight:700; font-size:13px; cursor:pointer; color:var(--mid); transition:all 0.15s; }
.login-tab.active { background:var(--ocean); border-color:var(--ocean); color:var(--white); }

/* ── HOME ── */
#s-home { background:var(--cream); padding-bottom:70px; }
.balance-card { margin:0 20px; background:var(--white); border-radius:var(--radius); padding:18px; box-shadow:0 4px 20px rgba(0,0,0,0.08); display:flex; align-items:center; justify-content:space-between; position:relative; overflow:hidden; }
.balance-card::before { content:'🌊'; position:absolute; right:-10px; bottom:-10px; font-size:70px; opacity:0.06; }
.balance-label { font-size:11px; color:var(--mid); font-weight:600; text-transform:uppercase; letter-spacing:0.5px; }
.balance-value { font-family:'Syne',sans-serif; font-size:26px; font-weight:800; color:var(--ocean); margin-top:3px; }
.balance-add { background:var(--ocean); color:var(--white); border:none; border-radius:10px; padding:9px 14px; font-weight:700; font-size:13px; cursor:pointer; }
.section-title { padding:18px 20px 10px; font-family:'Syne',sans-serif; font-size:17px; font-weight:700; color:var(--dark); }
.view-toggle { display:flex; gap:8px; padding:0 20px 12px; }
.view-btn { flex:1; padding:9px; border-radius:var(--radius-sm); border:2px solid var(--sand); background:var(--white); font-family:'Syne',sans-serif; font-weight:700; font-size:12px; cursor:pointer; color:var(--mid); transition:all 0.15s; }
.view-btn.active { background:var(--ocean); border-color:var(--ocean); color:var(--white); }
.kiosk-list { padding:0 20px; display:flex; flex-direction:column; gap:12px; }
.kiosk-card { background:var(--white); border-radius:var(--radius); overflow:hidden; box-shadow:0 2px 12px rgba(0,0,0,0.07); cursor:pointer; transition:transform 0.2s,box-shadow 0.2s; }
.kiosk-card:hover { transform:translateY(-3px); box-shadow:0 6px 20px rgba(0,0,0,0.12); }
.kiosk-img { height:110px; background:linear-gradient(135deg,var(--ocean-light,#1A7A9A),var(--wave)); display:flex; align-items:center; justify-content:center; font-size:44px; position:relative; }
.kiosk-badge { position:absolute; top:10px; right:10px; }
.kiosk-info { padding:12px 14px; }
.kiosk-name { font-family:'Syne',sans-serif; font-weight:700; font-size:15px; color:var(--dark); }
.kiosk-meta { font-size:12px; color:var(--mid); margin-top:3px; }
.kiosk-footer { display:flex; align-items:center; justify-content:space-between; margin-top:9px; }

/* MAP VIEW */
.map-view { display:none; padding:0 20px; }
.map-view.active { display:block; }
.map-placeholder { background:linear-gradient(135deg,var(--light),var(--sky)); border-radius:var(--radius); height:320px; display:flex; align-items:center; justify-content:center; flex-direction:column; gap:10px; position:relative; overflow:hidden; }
.map-pin { position:absolute; background:var(--ocean); color:var(--white); border-radius:50% 50% 50% 0; width:36px; height:36px; display:flex; align-items:center; justify-content:center; font-size:16px; transform:rotate(-45deg); box-shadow:0 3px 10px rgba(0,0,0,0.3); cursor:pointer; }
.map-pin span { transform:rotate(45deg); display:block; }
.map-pin.user { background:var(--yellow); }

/* ── MENU ── */
#s-menu { background:var(--cream); padding-bottom:130px; }
.time-picker { padding:14px 20px 0; }
.time-picker label { font-size:12px; font-weight:700; color:var(--mid); letter-spacing:0.5px; text-transform:uppercase; display:block; margin-bottom:8px; }
.time-slots { display:flex; gap:8px; flex-wrap:wrap; }
.time-slot { padding:8px 13px; border-radius:30px; border:2px solid var(--sand); background:var(--white); font-size:12px; font-weight:600; cursor:pointer; transition:all 0.15s; color:var(--mid); }
.time-slot.active { background:var(--ocean); border-color:var(--ocean); color:var(--white); }
.menu-cats { display:flex; gap:8px; padding:14px 20px 8px; overflow-x:auto; }
.menu-cats::-webkit-scrollbar { display:none; }
.cat-btn { padding:8px 14px; border-radius:30px; border:none; white-space:nowrap; background:var(--white); font-size:12px; font-weight:600; cursor:pointer; transition:all 0.15s; color:var(--mid); }
.cat-btn.active { background:var(--coral); color:var(--white); }
.menu-items { padding:0 20px; display:flex; flex-direction:column; gap:10px; }
.menu-item { background:var(--white); border-radius:var(--radius); padding:12px 14px; display:flex; align-items:center; gap:10px; box-shadow:0 2px 8px rgba(0,0,0,0.05); }
.item-emoji { font-size:34px; min-width:48px; text-align:center; }
.item-info { flex:1; }
.item-name { font-family:'Syne',sans-serif; font-weight:700; font-size:13px; color:var(--dark); }
.item-desc { font-size:11px; color:var(--mid); margin-top:2px; }
.item-prices { display:flex; align-items:center; gap:6px; margin-top:5px; }
.item-original { font-size:11px; color:var(--mid); text-decoration:line-through; }
.item-price { font-family:'Syne',sans-serif; font-weight:800; font-size:15px; color:var(--coral); }
.item-add-btn { width:34px; height:34px; border-radius:50%; background:var(--coral); border:none; color:var(--white); font-size:20px; cursor:pointer; display:flex; align-items:center; justify-content:center; box-shadow:0 3px 10px rgba(255,107,74,0.35); transition:all 0.15s; }
.item-qty { display:flex; align-items:center; gap:6px; }
.qty-btn { width:28px; height:28px; border-radius:50%; cursor:pointer; font-size:16px; font-weight:700; display:flex; align-items:center; justify-content:center; transition:all 0.15s; }
.qty-minus { border:2px solid var(--mid); color:var(--mid); background:transparent; }
.qty-minus:hover { border-color:var(--coral); color:var(--coral); }
.qty-plus { border:2px solid var(--coral); color:var(--coral); background:transparent; }
.qty-plus:hover { background:var(--coral); color:var(--white); }
.qty-num { font-weight:700; font-size:14px; color:var(--dark); min-width:18px; text-align:center; }

/* ── CHECKOUT ── */
#s-checkout { background:var(--cream); padding-bottom:90px; }
.checkout-body { padding:14px 20px; flex:1; }
.section-card { background:var(--white); border-radius:var(--radius); padding:14px; margin-bottom:12px; box-shadow:0 2px 8px rgba(0,0,0,0.05); }
.section-card h3 { font-family:'Syne',sans-serif; font-weight:700; font-size:14px; color:var(--dark); margin-bottom:10px; }
.order-line { display:flex; justify-content:space-between; align-items:center; padding:7px 0; border-bottom:1px solid var(--cream); }
.order-line:last-child { border-bottom:none; }
.order-line .name { font-size:13px; color:var(--dark); }
.order-line .qty-label { font-size:11px; color:var(--mid); }
.order-line .price { font-weight:700; color:var(--dark); font-size:13px; }
.price-row { display:flex; justify-content:space-between; font-size:13px; padding:4px 0; }
.price-row.discount { color:var(--success); font-weight:600; }
.price-row.fee { color:var(--mid); }
.price-row.total { font-family:'Syne',sans-serif; font-weight:800; font-size:17px; color:var(--dark); border-top:2px solid var(--cream); padding-top:9px; margin-top:4px; }
.pay-methods { display:flex; gap:8px; }
.pay-method { flex:1; padding:11px 6px; border-radius:var(--radius-sm); border:2px solid var(--sand); background:var(--white); cursor:pointer; text-align:center; transition:all 0.15s; }
.pay-method.active { border-color:var(--ocean); background:rgba(11,79,108,0.05); }
.pay-method .pm-icon { font-size:20px; margin-bottom:3px; }
.pay-method .pm-label { font-size:11px; font-weight:600; color:var(--mid); }
.pay-method.active .pm-label { color:var(--ocean); }
.checkout-footer { position:fixed; bottom:0; left:50%; transform:translateX(-50%); width:100%; max-width:480px; padding:14px 20px; background:rgba(245,230,200,0.97); backdrop-filter:blur(10px); }

/* ── TOKEN ── */
#s-token { background:linear-gradient(160deg,var(--ocean),var(--wave)); align-items:center; }
.token-body { padding:24px 20px; width:100%; display:flex; flex-direction:column; align-items:center; text-align:center; }
.token-check { width:72px; height:72px; border-radius:50%; background:var(--lime); display:flex; align-items:center; justify-content:center; font-size:32px; margin-bottom:14px; box-shadow:0 4px 20px rgba(200,232,50,0.4); }
.token-title { font-family:'Syne',sans-serif; font-weight:800; font-size:24px; color:var(--white); }
.token-sub { color:rgba(255,255,255,0.7); font-size:13px; margin-top:5px; margin-bottom:20px; }
.token-box { background:var(--white); border-radius:var(--radius); padding:20px; width:100%; max-width:300px; margin-bottom:14px; box-shadow:0 8px 30px rgba(0,0,0,0.2); }
.token-label { font-size:11px; color:var(--mid); text-transform:uppercase; letter-spacing:1px; font-weight:600; }
.token-number { font-family:'Syne',sans-serif; font-size:48px; font-weight:800; color:var(--ocean); letter-spacing:8px; margin:8px 0; }
.token-hint { font-size:12px; color:var(--mid); }
.token-qr { font-size:64px; margin:6px 0; }
.token-info { background:rgba(255,255,255,0.12); border-radius:var(--radius-sm); padding:12px 14px; width:100%; max-width:300px; margin-bottom:12px; }
.token-info-row { display:flex; justify-content:space-between; align-items:center; padding:5px 0; color:var(--white); font-size:12px; }
.token-info-row span:first-child { color:rgba(255,255,255,0.65); }
.token-info-row span:last-child { font-weight:600; }
.cancel-note { font-size:11px; color:rgba(255,255,255,0.5); max-width:260px; text-align:center; margin-top:6px; line-height:1.6; }
.token-btns { width:100%; max-width:300px; display:flex; flex-direction:column; gap:8px; margin-top:10px; }

/* ── CADASTRO ESTABELECIMENTO ── */
#s-cadastro { background:var(--cream); padding-bottom:80px; }
.cadastro-body { padding:16px 20px; }
.progress-bar { background:var(--sand); border-radius:10px; height:6px; margin-bottom:20px; overflow:hidden; }
.progress-fill { background:var(--ocean); height:100%; border-radius:10px; transition:width 0.3s; }
.section-progress { display:flex; justify-content:space-between; font-size:11px; color:var(--mid); margin-bottom:6px; }
.form-section { display:none; }
.form-section.active { display:block; }
.form-section-title { font-family:'Syne',sans-serif; font-weight:800; font-size:18px; color:var(--ocean); margin-bottom:16px; display:flex; align-items:center; gap:8px; }
.socios-list { display:flex; flex-direction:column; gap:10px; margin-bottom:10px; }
.socio-card { background:var(--white); border-radius:var(--radius-sm); padding:12px; border:1px solid var(--sand); position:relative; }
.socio-remove { position:absolute; top:8px; right:8px; background:var(--danger); color:var(--white); border:none; border-radius:50%; width:24px; height:24px; cursor:pointer; font-size:14px; display:flex; align-items:center; justify-content:center; }
.upload-btn { width:100%; padding:12px; border-radius:var(--radius-sm); border:2px dashed var(--sand); background:var(--white); font-family:'Syne',sans-serif; font-weight:600; font-size:13px; color:var(--mid); cursor:pointer; display:flex; align-items:center; justify-content:center; gap:8px; margin-bottom:8px; transition:all 0.15s; }
.upload-btn:hover { border-color:var(--ocean); color:var(--ocean); }
.upload-btn.uploaded { border-color:var(--success); color:var(--success); background:rgba(46,204,113,0.05); }
.nav-btns { display:flex; gap:10px; margin-top:16px; }
.section-nav { display:flex; gap:8px; justify-content:center; margin-bottom:16px; }
.section-dot { width:10px; height:10px; border-radius:50%; background:var(--sand); transition:all 0.2s; cursor:pointer; }
.section-dot.active { background:var(--ocean); transform:scale(1.3); }
.section-dot.done { background:var(--success); }

/* ── PAINEL QUIOSQUE ── */
#s-painel { background:var(--cream); }
.painel-tabs { display:flex; background:var(--white); border-bottom:2px solid var(--sand); }
.painel-tab { flex:1; padding:12px; border:none; background:transparent; cursor:pointer; font-family:'Syne',sans-serif; font-weight:700; font-size:12px; color:var(--mid); border-bottom:3px solid transparent; margin-bottom:-2px; transition:all 0.15s; }
.painel-tab.active { color:var(--ocean); border-bottom-color:var(--ocean); }
.painel-section { display:none; padding:14px 20px; padding-bottom:80px; }
.painel-section.active { display:block; }
.stats-row { display:flex; gap:8px; margin-bottom:14px; }
.stat-card { flex:1; background:var(--white); border-radius:var(--radius-sm); padding:12px 8px; text-align:center; box-shadow:0 2px 8px rgba(0,0,0,0.06); }
.stat-val { font-family:'Syne',sans-serif; font-size:22px; font-weight:800; color:var(--ocean); }
.stat-lbl { font-size:10px; color:var(--mid); margin-top:2px; }
.token-input-row { display:flex; gap:8px; margin-bottom:12px; }
.token-input { flex:1; padding:10px 12px; border-radius:var(--radius-sm); border:2px solid var(--sand); font-family:'Syne',sans-serif; font-size:20px; font-weight:700; letter-spacing:6px; text-align:center; color:var(--ocean); outline:none; }
.token-input:focus { border-color:var(--ocean); }
.token-ok-btn { padding:10px 16px; border-radius:var(--radius-sm); background:var(--ocean); border:none; color:var(--white); font-weight:700; font-size:14px; cursor:pointer; }
.order-card { background:var(--white); border-radius:var(--radius); padding:13px 15px; margin-bottom:10px; box-shadow:0 2px 8px rgba(0,0,0,0.06); }
.order-header { display:flex; justify-content:space-between; align-items:flex-start; margin-bottom:8px; }
.order-client { font-family:'Syne',sans-serif; font-weight:700; font-size:13px; color:var(--dark); }
.order-time { font-size:11px; color:var(--mid); margin-top:2px; }
.order-items-preview { font-size:12px; color:var(--mid); margin-bottom:8px; }
.order-footer { display:flex; justify-content:space-between; font-size:12px; margin-bottom:10px; }
.validate-btn { width:100%; padding:11px; border-radius:var(--radius-sm); background:linear-gradient(135deg,var(--coral),var(--coral-light)); border:none; color:var(--white); font-family:'Syne',sans-serif; font-weight:700; font-size:13px; cursor:pointer; transition:all 0.2s; }
.validate-btn.validated { background:linear-gradient(135deg,var(--success),#27AE60); cursor:default; }
.bar-chart { display:flex; align-items:flex-end; gap:8px; height:100px; padding:10px 0; }
.bar-item { flex:1; display:flex; flex-direction:column; align-items:center; gap:4px; }
.bar-fill { width:100%; border-radius:4px 4px 0 0; transition:height 0.3s; }
.bar-label { font-size:10px; color:var(--mid); }
.bar-val { font-size:11px; font-weight:700; color:var(--ocean); }
.toggle-row { display:flex; align-items:center; justify-content:space-between; padding:12px 0; border-bottom:1px solid var(--cream); }
.toggle-label { font-size:13px; font-weight:600; color:var(--dark); }
.toggle-sub { font-size:11px; color:var(--mid); margin-top:2px; }
.toggle-switch { position:relative; width:48px; height:26px; }
.toggle-switch input { opacity:0; width:0; height:0; }
.toggle-slider { position:absolute; cursor:pointer; inset:0; background:var(--sand); border-radius:26px; transition:.3s; }
.toggle-slider:before { position:absolute; content:''; height:20px; width:20px; left:3px; bottom:3px; background:var(--white); border-radius:50%; transition:.3s; }
input:checked + .toggle-slider { background:var(--ocean); }
input:checked + .toggle-slider:before { transform:translateX(22px); }
.finance-row { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid var(--cream); font-size:13px; }
.finance-val { font-weight:700; color:var(--ocean); }
.antecip-box { background:var(--light); border-radius:var(--radius-sm); padding:14px; margin:12px 0; }
.antecip-total { font-family:'Syne',sans-serif; font-size:26px; font-weight:800; color:var(--ocean); }
.antecip-fee { font-size:12px; color:var(--mid); margin-top:3px; }

/* ── WALLET ── */
#s-wallet { background:var(--cream); padding-bottom:80px; }
.wallet-hero { padding:30px 20px 50px; background:linear-gradient(160deg,var(--ocean),var(--wave)); position:relative; text-align:center; }
.wallet-hero::after { content:''; position:absolute; bottom:-2px; left:0; right:0; height:45px; background:var(--cream); clip-path:ellipse(65% 100% at 50% 100%); }
.wallet-balance { font-family:'Syne',sans-serif; font-size:42px; font-weight:800; color:var(--white); }
.wallet-label { font-size:13px; color:rgba(255,255,255,0.7); margin-bottom:6px; }
.quick-add { display:flex; gap:8px; }
.quick-btn { flex:1; padding:9px; border-radius:var(--radius-sm); border:2px solid var(--sand); background:var(--white); font-family:'Syne',sans-serif; font-weight:700; font-size:13px; cursor:pointer; color:var(--ocean); }
.quick-btn:hover { background:var(--ocean); color:var(--white); border-color:var(--ocean); }
.tx-item { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid var(--cream); }
.tx-icon { width:36px; height:36px; border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:16px; margin-right:10px; }
.tx-info { flex:1; }
.tx-name { font-size:13px; font-weight:600; color:var(--dark); }
.tx-date { font-size:11px; color:var(--mid); }
.tx-val { font-weight:700; font-size:14px; }
.tx-val.plus { color:var(--success); }
.tx-val.minus { color:var(--coral); }

/* ── ORDERS ── */
#s-orders { background:var(--cream); padding-bottom:80px; }
.order-status-card { background:var(--white); border-radius:var(--radius); padding:14px; margin-bottom:10px; box-shadow:0 2px 8px rgba(0,0,0,0.06); }
.os-header { display:flex; justify-content:space-between; margin-bottom:8px; }
.os-kiosk { font-family:'Syne',sans-serif; font-weight:700; font-size:14px; color:var(--dark); }
.os-items { font-size:12px; color:var(--mid); margin-bottom:8px; }
.os-footer { display:flex; justify-content:space-between; align-items:center; }
.os-token { font-size:12px; color:var(--mid); }
.os-token strong { color:var(--ocean); font-size:14px; }
.os-total { font-family:'Syne',sans-serif; font-weight:800; font-size:14px; color:var(--ocean); }
</style>
</head>
<body>

<!-- ══ SPLASH ══ -->
<div class="screen active" id="s-splash">
  <div class="splash-content">
    <div class="splash-icon">🏖️</div>
    <div class="splash-logo">Pede<span>Fácil</span></div>
    <p class="splash-sub">Peça antes. Curta mais.</p>
    <div class="splash-features">
      <div class="splash-feat"><div class="fi">⏰</div><div class="fl">Pedido antecipado</div></div>
      <div class="splash-feat"><div class="fi">💸</div><div class="fl">10% desconto</div></div>
      <div class="splash-feat"><div class="fi">🔑</div><div class="fl">Token de resgate</div></div>
    </div>
    <div class="splash-btns">
      <button class="btn btn-primary" onclick="go('s-login','cliente')">Entrar como Cliente</button>
      <button class="btn btn-white btn-sm" onclick="go('s-login','estab')" style="margin-top:4px">Sou Estabelecimento</button>
    </div>
  </div>
</div>

<!-- ══ LOGIN ══ -->
<div class="screen" id="s-login">
  <div class="login-header">
    <div class="topbar" style="background:transparent;padding:0 0 16px">
      <button class="back-btn" onclick="go('s-splash')">←</button>
      <div class="logo" style="color:white;font-size:20px">Pede<span style="color:var(--yellow)">Fácil</span></div>
      <div style="width:40px"></div>
    </div>
    <h2 id="login-title">Bem-vindo! 👋</h2>
    <p id="login-sub">Entre com seu CPF ou e-mail</p>
  </div>
  <div class="login-body">
    <div class="login-tabs">
      <button class="login-tab active" onclick="loginTab(this,'tab-login')">Entrar</button>
      <button class="login-tab" onclick="loginTab(this,'tab-cadastro')">Criar conta</button>
    </div>
    <div id="tab-login">
      <div class="input-group"><label>CPF ou E-mail</label><input type="text" placeholder="000.000.000-00" id="login-cpf"></div>
      <div class="input-group"><label>Senha</label><input type="password" placeholder="••••••••"></div>
      <button class="btn btn-primary" onclick="doLogin()" style="margin-top:8px">Entrar</button>
      <div class="login-divider">ou</div>
      <button class="btn btn-outline btn-sm" onclick="doLogin()">📱 Entrar com Google</button>
    </div>
    <div id="tab-cadastro" style="display:none">
      <div class="input-group"><label>Nome completo</label><input type="text" placeholder="Seu nome"></div>
      <div class="input-group"><label>CPF</label><input type="text" placeholder="000.000.000-00"></div>
      <div class="input-group"><label>E-mail</label><input type="email" placeholder="seu@email.com"></div>
      <div class="input-group"><label>Telefone</label><input type="tel" placeholder="(00) 00000-0000"></div>
      <div class="input-group"><label>Senha</label><input type="password" placeholder="••••••••"></div>
      <div style="display:flex;align-items:flex-start;gap:8px;margin-bottom:14px">
        <input type="checkbox" id="aceite" style="margin-top:3px;width:auto">
        <label for="aceite" style="font-size:12px;color:var(--mid)">Li e aceito os <a href="#" style="color:var(--ocean)">Termos de Uso</a> e a <a href="#" style="color:var(--ocean)">Política de Privacidade</a></label>
      </div>
      <button class="btn btn-primary" onclick="doLogin()">Criar conta grátis</button>
    </div>
    <div style="margin-top:20px;padding:12px;background:rgba(11,79,108,0.06);border-radius:var(--radius-sm)">
      <p style="font-size:12px;color:var(--mid);line-height:1.6">💡 <strong>Carteira PedeFácil:</strong> Seu saldo fica salvo aqui. Perfeito para ir à praia sem cartão!</p>
    </div>
  </div>
</div>

<!-- ══ HOME ══ -->
<div class="screen" id="s-home">
  <div class="hero">
    <div class="topbar" style="background:transparent;padding:0 0 8px">
      <div class="logo" style="color:white;font-size:20px">Pede<span style="color:var(--yellow)">Fácil</span></div>
      <div style="display:flex;gap:8px">
        <button class="back-btn" onclick="openModal('modal-orders-preview')" title="Pedidos">📋</button>
        <button class="back-btn" onclick="go('s-splash')" title="Sair">👤</button>
      </div>
    </div>
    <h2>Olá, Marcelo! ☀️</h2>
    <p>Onde você vai curtir hoje?</p>
  </div>
  <div style="margin-top:16px">
    <div class="balance-card" onclick="go('s-wallet')">
      <div>
        <div class="balance-label">Saldo PedeFácil</div>
        <div class="balance-value">R$ 85,00</div>
      </div>
      <button class="balance-add" onclick="event.stopPropagation();openModal('modal-recharge')">+ Adicionar</button>
    </div>
    <div class="section-title">🏖️ Quiosques perto de você</div>
    <div class="view-toggle">
      <button class="view-btn active" id="btn-list" onclick="switchView('list')">📋 Lista</button>
      <button class="view-btn" id="btn-map" onclick="switchView('map')">🗺️ Mapa</button>
    </div>
    <div id="view-list" class="kiosk-list">
      <div class="kiosk-card" onclick="go('s-menu')">
        <div class="kiosk-img" style="background:linear-gradient(135deg,#0B4F6C,#22B5D4)">🌊
          <div class="kiosk-badge"><span class="tag tag-lime">10% OFF</span></div>
        </div>
        <div class="kiosk-info">
          <div class="kiosk-name">Quiosque Maresias</div>
          <div class="kiosk-meta">📍 Praia de Caldas Novas, GO · Aberto agora</div>
          <div class="kiosk-footer">
            <div style="display:flex;gap:5px"><span class="tag tag-ocean" style="font-size:10px">🍤 Frutos do Mar</span><span class="tag tag-ocean" style="font-size:10px">🍺 Bebidas</span></div>
            <span style="font-size:12px;color:var(--coral);font-weight:600">⭐ 4.8</span>
          </div>
        </div>
      </div>
      <div class="kiosk-card" onclick="go('s-menu')">
        <div class="kiosk-img" style="background:linear-gradient(135deg,#FF6B4A,#FF8B6E)">🌴
          <div class="kiosk-badge"><span class="tag tag-lime">10% OFF</span></div>
        </div>
        <div class="kiosk-info">
          <div class="kiosk-name">Barraca do Sol</div>
          <div class="kiosk-meta">📍 Parque das Águas, GO · Aberto agora</div>
          <div class="kiosk-footer">
            <div style="display:flex;gap:5px"><span class="tag tag-ocean" style="font-size:10px">🌮 Petiscos</span><span class="tag tag-ocean" style="font-size:10px">🥤 Sucos</span></div>
            <span style="font-size:12px;color:var(--coral);font-weight:600">⭐ 4.6</span>
          </div>
        </div>
      </div>
      <div class="kiosk-card" onclick="go('s-menu')">
        <div class="kiosk-img" style="background:linear-gradient(135deg,#1A7A9A,#C8E832)">🏄
        </div>
        <div class="kiosk-info">
          <div class="kiosk-name">Kiosque Ondas</div>
          <div class="kiosk-meta">📍 Rio Quente Resorts, GO · Aberto agora</div>
          <div class="kiosk-footer">
            <div style="display:flex;gap:5px"><span class="tag tag-ocean" style="font-size:10px">🍗 Frango</span><span class="tag tag-ocean" style="font-size:10px">🍺 Cervejas</span></div>
            <span style="font-size:12px;color:var(--mid);font-weight:600">Sem desconto hoje</span>
          </div>
        </div>
      </div>
    </div>
    <div id="view-map" class="map-view" style="padding:0 20px">
      <div class="map-placeholder">
        <div style="font-size:14px;color:var(--mid);font-weight:600;z-index:1">🗺️ Mapa dos Quiosques</div>
        <div style="font-size:12px;color:var(--mid);z-index:1">Região de Goiás</div>
        <div class="map-pin" style="top:35%;left:40%" onclick="go('s-menu')"><span>🏖️</span></div>
        <div class="map-pin" style="top:55%;left:60%" onclick="go('s-menu')"><span>🌴</span></div>
        <div class="map-pin" style="top:45%;left:25%" onclick="go('s-menu')"><span>🏄</span></div>
        <div class="map-pin user" style="top:50%;left:45%"><span>📍</span></div>
      </div>
      <p style="font-size:11px;color:var(--mid);text-align:center;margin-top:8px">Toque em um pin para ver o quiosque</p>
    </div>
  </div>
  <div style="height:80px"></div>
  <nav class="bottom-nav">
    <button class="nav-btn active" onclick="go('s-home')"><span class="ni">🏠</span>Início</button>
    <button class="nav-btn" onclick="go('s-orders')"><span class="ni">📋</span>Pedidos</button>
    <button class="nav-btn" onclick="go('s-wallet')"><span class="ni">💳</span>Carteira</button>
    <button class="nav-btn" onclick="openModal('modal-profile')"><span class="ni">👤</span>Perfil</button>
  </nav>
</div>

<!-- ══ MENU ══ -->
<div class="screen" id="s-menu">
  <div class="hero">
    <div class="topbar" style="background:transparent;padding:0 0 8px">
      <button class="back-btn" onclick="go('s-home')">←</button>
      <div class="logo" style="color:white;font-size:17px">Quiosque <span style="color:var(--yellow)">Maresias</span></div>
      <div style="width:40px"></div>
    </div>
    <h2>Cardápio 🍽️</h2>
    <p>⭐ 4.8 · 📍 Caldas Novas, GO</p>
  </div>
  <div class="time-picker" style="padding:14px 20px 0">
    <label>🕐 Quando você vai chegar?</label>
    <div class="time-slots">
      <div class="time-slot active" onclick="selectTime(this,'11h–12h')">11h–12h</div>
      <div class="time-slot" onclick="selectTime(this,'12h–13h')">12h–13h</div>
      <div class="time-slot" onclick="selectTime(this,'13h–14h')">13h–14h</div>
      <div class="time-slot" onclick="selectTime(this,'14h–15h')">14h–15h</div>
      <div class="time-slot" onclick="selectTime(this,'15h–16h')">15h–16h</div>
    </div>
  </div>
  <div class="menu-cats">
    <button class="cat-btn active" onclick="filterCat(this,'all')">Todos</button>
    <button class="cat-btn" onclick="filterCat(this,'comida')">🍽️ Comida</button>
    <button class="cat-btn" onclick="filterCat(this,'bebida')">🍺 Bebidas</button>
    <button class="cat-btn" onclick="filterCat(this,'petisco')">🍟 Petiscos</button>
  </div>
  <div class="menu-items" id="menu-items"></div>
  <div class="cart-bar" id="cart-bar" onclick="go('s-checkout')">
    <div style="display:flex;align-items:center;gap:10px">
      <div class="cart-badge" id="cart-badge">0</div>
      <span style="color:var(--white);font-weight:600;font-size:14px">Ver pedido</span>
    </div>
    <div class="cart-total" id="cart-total">R$ 0,00</div>
  </div>
  <div style="height:70px"></div>
</div>

<!-- ══ CHECKOUT ══ -->
<div class="screen" id="s-checkout">
  <div class="hero" style="padding-bottom:40px">
    <div class="topbar" style="background:transparent;padding:0 0 8px">
      <button class="back-btn" onclick="go('s-menu')">←</button>
      <div class="logo" style="color:white;font-size:18px">Revisão do <span style="color:var(--yellow)">Pedido</span></div>
      <div style="width:40px"></div>
    </div>
  </div>
  <div class="checkout-body">
    <div class="section-card">
      <h3>🛒 Itens do pedido</h3>
      <div id="checkout-items"></div>
    </div>
    <div class="section-card">
      <h3>🕐 Horário de chegada</h3>
      <div style="display:flex;align-items:center;gap:10px">
        <span style="font-size:24px">🏖️</span>
        <div>
          <div style="font-weight:700;color:var(--ocean);font-size:14px" id="checkout-time">11h – 12h</div>
          <div style="font-size:11px;color:var(--mid)">Quiosque Maresias · Caldas Novas</div>
        </div>
      </div>
    </div>
    <div class="section-card" style="border:2px solid var(--lime)">
      <h3>🎉 Desconto antecipado</h3>
      <div id="price-breakdown"></div>
    </div>
    <div class="section-card">
      <h3>💳 Forma de pagamento</h3>
      <div class="pay-methods">
        <div class="pay-method active" onclick="selectPay(this,'saldo')">
          <div class="pm-icon">💰</div>
          <div class="pm-label">Saldo<br>R$ 85,00</div>
        </div>
        <div class="pay-method" onclick="selectPay(this,'pix')">
          <div class="pm-icon">⚡</div>
          <div class="pm-label">Pix</div>
        </div>
        <div class="pay-method" onclick="selectPay(this,'credito')">
          <div class="pm-icon">💳</div>
          <div class="pm-label">Crédito</div>
        </div>
      </div>
      <p style="font-size:11px;color:var(--mid);margin-top:8px;font-style:italic" id="pay-note">✅ Sem taxa adicional ao usar Saldo PedeFácil</p>
    </div>
    <div style="padding:10px 12px;background:rgba(11,79,108,0.06);border-radius:var(--radius-sm)">
      <p style="font-size:11px;color:var(--mid);line-height:1.6">📋 <strong>Cancelamento:</strong> 100% antes do token ser validado. Após validação: 80% cliente · 10% quiosque · 10% plataforma.</p>
    </div>
  </div>
  <div class="checkout-footer">
    <button class="btn btn-primary" onclick="go('s-token')">🔑 Confirmar e gerar token</button>
  </div>
</div>

<!-- ══ TOKEN ══ -->
<div class="screen" id="s-token">
  <div class="topbar" style="background:transparent;padding:20px 20px 0">
    <button class="back-btn" style="background:rgba(255,255,255,0.2)" onclick="go('s-home')">🏠</button>
    <div class="logo" style="color:white;font-size:18px">Pede<span style="color:var(--yellow)">Fácil</span></div>
    <div style="width:40px"></div>
  </div>
  <div class="token-body">
    <div class="token-check">✅</div>
    <div class="token-title">Pedido confirmado!</div>
    <div class="token-sub">Apresente seu token no quiosque</div>
    <div class="token-box">
      <div class="token-label">Token de resgate</div>
      <div class="token-number" id="token-display">4827</div>
      <div class="token-hint">ou mostre o QR Code</div>
      <div class="token-qr">▓▒░▒▓</div>
      <div style="font-size:11px;color:var(--mid)">CPF: •••.456.•••-12</div>
    </div>
    <div class="token-info">
      <div class="token-info-row"><span>📍 Local</span><span>Quiosque Maresias</span></div>
      <div class="token-info-row"><span>🕐 Horário</span><span id="token-time">11h – 12h</span></div>
      <div class="token-info-row"><span>💰 Total</span><span id="token-total">R$ 0,00</span></div>
      <div class="token-info-row"><span>🏷️ Desconto</span><span style="color:var(--lime)">10% aplicado</span></div>
      <div class="token-info-row"><span>📦 Status</span><span>Aguardando validação</span></div>
    </div>
    <p class="cancel-note">⚠️ Token não validado ainda. Cancelamento = 100% de reembolso</p>
    <div class="token-btns">
      <button class="btn btn-white btn-sm" onclick="openModal('modal-share')">📤 Compartilhar token</button>
      <button class="btn btn-white btn-sm" style="opacity:0.7" onclick="go('s-home')">🏠 Voltar ao início</button>
    </div>
  </div>
</div>

<!-- ══ CADASTRO ESTABELECIMENTO ══ -->
<div class="screen" id="s-cadastro">
  <div class="hero" style="padding-bottom:40px">
    <div class="topbar" style="background:transparent;padding:0 0 8px">
      <button class="back-btn" onclick="go('s-splash')">←</button>
      <div class="logo" style="color:white;font-size:16px">Cadastro do <span style="color:var(--yellow)">Estabelecimento</span></div>
      <div style="width:40px"></div>
    </div>
  </div>
  <div class="cadastro-body">
    <div class="section-progress">
      <span id="step-label">Passo 1 de 6 — Dados da Empresa</span>
      <span id="step-pct">17%</span>
    </div>
    <div class="progress-bar"><div class="progress-fill" id="prog-fill" style="width:17%"></div></div>
    <div class="section-nav" id="step-dots"></div>

    <!-- SEÇÃO 1 -->
    <div class="form-section active" id="fs-1">
      <div class="form-section-title">🏢 Dados da Empresa</div>
      <div class="input-group"><label>Razão Social</label><input type="text" placeholder="Nome empresarial completo"></div>
      <div class="input-group"><label>Nome Fantasia</label><input type="text" placeholder="Como aparece para o cliente"></div>
      <div class="input-group"><label>CNPJ</label><input type="text" placeholder="00.000.000/0000-00" id="cnpj-field" oninput="maskCNPJ(this)"></div>
      <div class="input-group"><label>Inscrição Estadual</label><input type="text" placeholder="Opcional"></div>
      <div class="input-group"><label>Data de Abertura</label><input type="date"></div>
      <div class="input-group"><label>Categoria</label>
        <select>
          <option>Selecione...</option>
          <option>Quiosque de Praia</option>
          <option>Barraca de Praia</option>
          <option>Quiosque de Parque</option>
          <option>Restaurante</option>
          <option>Bar</option>
        </select>
      </div>
    </div>

    <!-- SEÇÃO 2 -->
    <div class="form-section" id="fs-2">
      <div class="form-section-title">👤 Responsável Legal</div>
      <div class="input-group"><label>Nome Completo</label><input type="text" placeholder="Nome do responsável"></div>
      <div class="input-group"><label>CPF</label><input type="text" placeholder="000.000.000-00"></div>
      <div class="input-group"><label>Cargo / Função</label><input type="text" placeholder="Ex: Sócio-Gerente"></div>
      <div class="input-group"><label>E-mail</label><input type="email" placeholder="responsavel@email.com"></div>
      <div class="input-group"><label>Celular</label><input type="tel" placeholder="(00) 00000-0000"></div>
      <div class="input-group"><label>Telefone Comercial</label><input type="tel" placeholder="(00) 0000-0000"></div>
    </div>

    <!-- SEÇÃO 3 -->
    <div class="form-section" id="fs-3">
      <div class="form-section-title">📍 Endereço</div>
      <div style="display:flex;gap:8px">
        <div class="input-group" style="flex:1"><label>CEP</label><input type="text" placeholder="00000-000" oninput="maskCEP(this)"></div>
        <button class="btn btn-ocean btn-sm" style="width:auto;align-self:flex-end;margin-bottom:14px;white-space:nowrap" onclick="buscarCEP()">🔍 Buscar</button>
      </div>
      <div class="input-group"><label>Logradouro</label><input type="text" placeholder="Rua / Avenida" id="logradouro"></div>
      <div style="display:flex;gap:8px">
        <div class="input-group" style="flex:1"><label>Número</label><input type="text" placeholder="Nº"></div>
        <div class="input-group" style="flex:2"><label>Complemento</label><input type="text" placeholder="Sala, Loja..."></div>
      </div>
      <div class="input-group"><label>Bairro</label><input type="text" placeholder="Bairro" id="bairro"></div>
      <div style="display:flex;gap:8px">
        <div class="input-group" style="flex:2"><label>Cidade</label><input type="text" placeholder="Cidade" id="cidade"></div>
        <div class="input-group" style="flex:1"><label>Estado</label>
          <select id="estado">
            <option>GO</option><option>SP</option><option>RJ</option><option>MG</option>
            <option>BA</option><option>RS</option><option>PR</option><option>SC</option>
          </select>
        </div>
      </div>
    </div>

    <!-- SEÇÃO 4 -->
    <div class="form-section" id="fs-4">
      <div class="form-section-title">👥 Quadro de Sócios</div>
      <div class="socios-list" id="socios-list">
        <div class="socio-card">
          <div style="font-size:12px;font-weight:700;color:var(--ocean);margin-bottom:8px">Sócio 1</div>
          <div class="input-group"><label>Nome</label><input type="text" placeholder="Nome completo"></div>
          <div style="display:flex;gap:8px">
            <div class="input-group" style="flex:2"><label>CPF</label><input type="text" placeholder="000.000.000-00"></div>
            <div class="input-group" style="flex:1"><label>Participação</label><input type="text" placeholder="100%"></div>
          </div>
          <div class="input-group"><label>Cargo</label><input type="text" placeholder="Sócio-Gerente"></div>
        </div>
      </div>
      <button class="btn btn-outline btn-sm" onclick="addSocio()" style="width:auto;padding:10px 20px">+ Adicionar Sócio</button>
    </div>

    <!-- SEÇÃO 5 -->
    <div class="form-section" id="fs-5">
      <div class="form-section-title">🏦 Dados Bancários</div>
      <div class="input-group"><label>Banco</label>
        <select>
          <option>Selecione o banco...</option>
          <option>001 - Banco do Brasil</option>
          <option>033 - Santander</option>
          <option>104 - Caixa Econômica</option>
          <option>237 - Bradesco</option>
          <option>341 - Itaú</option>
          <option>756 - Sicoob</option>
          <option>077 - Banco Inter</option>
          <option>260 - NuBank</option>
          <option>323 - Mercado Pago</option>
          <option>274 - InfinityPay</option>
        </select>
      </div>
      <div style="display:flex;gap:8px">
        <div class="input-group" style="flex:1"><label>Agência</label><input type="text" placeholder="0000"></div>
        <div class="input-group" style="flex:2"><label>Conta</label><input type="text" placeholder="00000-0"></div>
      </div>
      <div class="input-group"><label>Tipo de conta</label>
        <select><option>Conta Corrente</option><option>Conta Poupança</option><option>Conta de Pagamento</option></select>
      </div>
      <div class="input-group"><label>Tipo de Chave Pix</label>
        <select id="pix-type" onchange="updatePixPlaceholder()">
          <option value="cpf">CPF</option>
          <option value="cnpj">CNPJ</option>
          <option value="email">E-mail</option>
          <option value="tel">Telefone</option>
          <option value="random">Chave Aleatória</option>
        </select>
      </div>
      <div class="input-group"><label>Chave Pix</label><input type="text" placeholder="000.000.000-00" id="pix-key"></div>
    </div>

    <!-- SEÇÃO 6 -->
    <div class="form-section" id="fs-6">
      <div class="form-section-title">📄 Documentos</div>
      <p style="font-size:12px;color:var(--mid);margin-bottom:14px;line-height:1.6">Envie os documentos do estabelecimento. Formatos aceitos: PDF, JPG, PNG (máx. 10MB cada)</p>
      <button class="upload-btn" onclick="markUploaded(this,'Contrato Social / Requerimento de Empresário')">📎 Contrato Social / Req. Empresário</button>
      <button class="upload-btn" onclick="markUploaded(this,'Cartão CNPJ')">📎 Cartão CNPJ</button>
      <button class="upload-btn" onclick="markUploaded(this,'RG / CNH do Responsável')">📎 RG / CNH do Responsável</button>
      <button class="upload-btn" onclick="markUploaded(this,'Alvará de Funcionamento')">📎 Alvará de Funcionamento</button>
      <button class="upload-btn" onclick="markUploaded(this,'Licença Sanitária')">📎 Licença Sanitária</button>
      <div style="margin-top:12px;padding:12px;background:rgba(46,204,113,0.08);border-radius:var(--radius-sm);border:1px solid rgba(46,204,113,0.2)">
        <p style="font-size:12px;color:var(--mid);line-height:1.6">✅ Após enviar o cadastro, nossa equipe analisará os documentos em até <strong>2 dias úteis</strong>. Você será notificado por e-mail.</p>
      </div>
      <button class="btn btn-primary" style="margin-top:16px" onclick="submitCadastro()">🚀 Enviar cadastro para análise</button>
    </div>

    <div class="nav-btns">
      <button class="btn btn-outline btn-sm" id="btn-prev" onclick="prevStep()" style="display:none;width:auto;padding:10px 20px">← Anterior</button>
      <button class="btn btn-ocean btn-sm" id="btn-next" onclick="nextStep()" style="width:auto;padding:10px 24px;margin-left:auto">Próximo →</button>
    </div>
  </div>
</div>

<!-- ══ PAINEL QUIOSQUE ══ -->
<div class="screen" id="s-painel">
  <div class="hero" style="padding-bottom:40px">
    <div class="topbar" style="background:transparent;padding:0 0 8px">
      <button class="back-btn" onclick="go('s-splash')">←</button>
      <div class="logo" style="color:white;font-size:17px">Painel <span style="color:var(--yellow)">Quiosque</span></div>
      <div style="width:40px"></div>
    </div>
    <h2>Quiosque Maresias 🏖️</h2>
    <p id="painel-date">Carregando...</p>
  </div>
  <div class="painel-tabs">
    <button class="painel-tab active" onclick="painelTab(this,'pt-orders')">📋 Pedidos</button>
    <button class="painel-tab" onclick="painelTab(this,'pt-forecast')">📊 Previsão</button>
    <button class="painel-tab" onclick="painelTab(this,'pt-finance')">💰 Finanças</button>
  </div>

  <!-- PEDIDOS -->
  <div class="painel-section active" id="pt-orders">
    <div class="stats-row">
      <div class="stat-card"><div class="stat-val">12</div><div class="stat-lbl">Pedidos hoje</div></div>
      <div class="stat-card"><div class="stat-val" id="pendentes-count">5</div><div class="stat-lbl">Pendentes</div></div>
      <div class="stat-card"><div class="stat-val" id="validados-count">7</div><div class="stat-lbl">Validados</div></div>
    </div>
    <div class="section-title" style="padding-top:6px">🔑 Validar token</div>
    <div class="token-input-row">
      <input class="token-input" type="text" placeholder="0000" maxlength="4" id="token-val-input">
      <button class="token-ok-btn" onclick="validateToken()">✓ OK</button>
    </div>
    <div class="section-title" style="padding-top:2px">📋 Pedidos de hoje</div>
    <div id="orders-list">
      <div class="order-card" id="oc-1">
        <div class="order-header">
          <div><div class="order-client">João Silva</div><div class="order-time">🕐 11h–12h · CPF: •••.456.•••-12</div></div>
          <span class="tag tag-coral" id="ob-1">Pendente</span>
        </div>
        <div class="order-items-preview">🍤 Camarão grelhado (1) · 🍺 Cerveja gelada (2)</div>
        <div class="order-footer">
          <span style="color:var(--mid)">Token: <strong style="color:var(--ocean)">4827</strong></span>
          <span style="font-weight:700">R$ 67,50</span>
        </div>
        <button class="validate-btn" id="vb-1" onclick="validateOrder(1,'4827')">🔑 Validar token e iniciar preparo</button>
      </div>
      <div class="order-card" id="oc-2">
        <div class="order-header">
          <div><div class="order-client">Maria Santos</div><div class="order-time">🕐 12h–13h · CPF: •••.789.•••-33</div></div>
          <span class="tag tag-coral" id="ob-2">Pendente</span>
        </div>
        <div class="order-items-preview">🌮 Combo petisco (2) · 🥤 Suco natural (1)</div>
        <div class="order-footer">
          <span style="color:var(--mid)">Token: <strong style="color:var(--ocean)">3591</strong></span>
          <span style="font-weight:700">R$ 45,00</span>
        </div>
        <button class="validate-btn" id="vb-2" onclick="validateOrder(2,'3591')">🔑 Validar token e iniciar preparo</button>
      </div>
      <div class="order-card">
        <div class="order-header">
          <div><div class="order-client">Pedro Oliveira</div><div class="order-time">🕐 14h–15h · CPF: •••.123.•••-77</div></div>
          <span class="tag tag-success">Validado ✓</span>
        </div>
        <div class="order-items-preview">🍺 Cerveja (3) · 🥥 Água de coco (1)</div>
        <div class="order-footer">
          <span style="color:var(--mid)">Token: <strong style="color:var(--success)">7014</strong></span>
          <span style="font-weight:700;color:var(--success)">R$ 38,00 ✓</span>
        </div>
        <button class="validate-btn validated" disabled>✅ Preparo iniciado · Crédito liberado</button>
      </div>
    </div>
  </div>

  <!-- PREVISÃO -->
  <div class="painel-section" id="pt-forecast">
    <div class="stats-row">
      <div class="stat-card"><div class="stat-val">R$ 892</div><div class="stat-lbl">Previsto hoje</div></div>
      <div class="stat-card"><div class="stat-val">23</div><div class="stat-lbl">Pedidos previstos</div></div>
    </div>
    <div class="card">
      <div class="card-title" style="margin-bottom:14px">📊 Demanda por horário</div>
      <div class="bar-chart">
        <div class="bar-item"><div class="bar-val">35%</div><div class="bar-fill" style="height:35px;background:var(--ocean)"></div><div class="bar-label">11-12h</div></div>
        <div class="bar-item"><div class="bar-val">78%</div><div class="bar-fill" style="height:78px;background:var(--coral)"></div><div class="bar-label">12-13h</div></div>
        <div class="bar-item"><div class="bar-val">60%</div><div class="bar-fill" style="height:60px;background:var(--sky)"></div><div class="bar-label">13-14h</div></div>
        <div class="bar-item"><div class="bar-val">50%</div><div class="bar-fill" style="height:50px;background:var(--wave)"></div><div class="bar-label">14-15h</div></div>
        <div class="bar-item"><div class="bar-val">30%</div><div class="bar-fill" style="height:30px;background:var(--ocean)"></div><div class="bar-label">15-16h</div></div>
      </div>
      <p style="font-size:11px;color:var(--mid);margin-top:10px">🍽️ Mais pedidos: Camarão (8x) · Cerveja gelada (15x)</p>
    </div>
  </div>

  <!-- FINANÇAS -->
  <div class="painel-section" id="pt-finance">
    <div class="stats-row">
      <div class="stat-card"><div class="stat-val">R$ 487</div><div class="stat-lbl">Validado hoje</div></div>
      <div class="stat-card"><div class="stat-val">R$ 405</div><div class="stat-lbl">A receber</div></div>
    </div>
    <div class="card">
      <div class="card-title" style="margin-bottom:10px">⚙️ Configurações</div>
      <div class="toggle-row">
        <div><div class="toggle-label">Desconto antecipado 10%</div><div class="toggle-sub">Clientes recebem 10% OFF</div></div>
        <label class="toggle-switch"><input type="checkbox" checked onchange="toggleDiscount(this)"><span class="toggle-slider"></span></label>
      </div>
      <div class="toggle-row">
        <div><div class="toggle-label">Quiosque ativo na plataforma</div><div class="toggle-sub">Visível para clientes</div></div>
        <label class="toggle-switch"><input type="checkbox" checked><span class="toggle-slider"></span></label>
      </div>
    </div>
    <div class="card">
      <div class="card-title" style="margin-bottom:10px">⚡ Antecipação via Pix</div>
      <div class="antecip-box">
        <div style="font-size:12px;color:var(--mid);margin-bottom:4px">Disponível para antecipar:</div>
        <div class="antecip-total">R$ 405,00</div>
        <div class="antecip-fee">Taxa D+0: 10% · Você recebe R$ 364,50</div>
      </div>
      <button class="btn btn-ocean btn-sm" onclick="openModal('modal-antecip')" style="width:100%">⚡ Solicitar antecipação</button>
    </div>
    <div class="card">
      <div class="card-title" style="margin-bottom:10px">💳 Tabela de taxas</div>
      <div class="finance-row"><span>Pix / Saldo PedeFácil</span><span class="finance-val">3%</span></div>
      <div class="finance-row"><span>Cartão de crédito</span><span class="finance-val">~6,8%</span></div>
      <div class="finance-row"><span>Antecipação D+0</span><span class="finance-val">10% + 3%</span></div>
      <div class="finance-row"><span style="color:var(--success)">Mensalidade (12 meses)</span><span class="finance-val" style="color:var(--success)">GRÁTIS ✓</span></div>
    </div>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn active" onclick="painelTab(document.querySelector('.painel-tab.active'),'pt-orders')"><span class="ni">📋</span>Pedidos</button>
    <button class="nav-btn" onclick="go('s-cadastro')"><span class="ni">📝</span>Cadastro</button>
    <button class="nav-btn" onclick="openModal('modal-settings')"><span class="ni">⚙️</span>Config</button>
  </nav>
</div>

<!-- ══ WALLET ══ -->
<div class="screen" id="s-wallet">
  <div class="wallet-hero">
    <div class="topbar" style="background:transparent;padding:0 0 12px">
      <button class="back-btn" onclick="go('s-home')">←</button>
      <div class="logo" style="color:white;font-size:18px">Pede<span style="color:var(--yellow)">Fácil</span></div>
      <div style="width:40px"></div>
    </div>
    <div class="wallet-label">Saldo disponível</div>
    <div class="wallet-balance">R$ 85,00</div>
  </div>
  <div style="padding:20px 20px 0">
    <button class="btn btn-primary" onclick="openModal('modal-recharge')" style="margin-bottom:16px">+ Adicionar saldo</button>
    <div class="section-title" style="padding:0 0 10px">Adicionar rapidinho:</div>
    <div class="quick-add" style="margin-bottom:20px">
      <button class="quick-btn">R$ 50</button>
      <button class="quick-btn">R$ 100</button>
      <button class="quick-btn">R$ 200</button>
    </div>
    <div class="section-title" style="padding:0 0 10px">Últimas movimentações:</div>
    <div class="tx-item">
      <div style="display:flex;align-items:center">
        <div class="tx-icon" style="background:rgba(46,204,113,0.1)">➕</div>
        <div class="tx-info"><div class="tx-name">Recarga via Pix</div><div class="tx-date">Hoje, 10:30</div></div>
      </div>
      <div class="tx-val plus">+R$ 100,00</div>
    </div>
    <div class="tx-item">
      <div style="display:flex;align-items:center">
        <div class="tx-icon" style="background:rgba(255,107,74,0.1)">🛒</div>
        <div class="tx-info"><div class="tx-name">Pedido Quiosque Maresias</div><div class="tx-date">Hoje, 09:15</div></div>
      </div>
      <div class="tx-val minus">-R$ 15,00</div>
    </div>
  </div>
  <div style="height:80px"></div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="go('s-home')"><span class="ni">🏠</span>Início</button>
    <button class="nav-btn" onclick="go('s-orders')"><span class="ni">📋</span>Pedidos</button>
    <button class="nav-btn active"><span class="ni">💳</span>Carteira</button>
    <button class="nav-btn" onclick="openModal('modal-profile')"><span class="ni">👤</span>Perfil</button>
  </nav>
</div>

<!-- ══ ORDERS ══ -->
<div class="screen" id="s-orders">
  <div class="hero" style="padding-bottom:40px">
    <div class="topbar" style="background:transparent;padding:0 0 8px">
      <button class="back-btn" onclick="go('s-home')">←</button>
      <div class="logo" style="color:white;font-size:18px">Meus <span style="color:var(--yellow)">Pedidos</span></div>
      <div style="width:40px"></div>
    </div>
  </div>
  <div style="padding:16px 20px;padding-bottom:80px">
    <div class="order-status-card">
      <div class="os-header"><div class="os-kiosk">Quiosque Maresias</div><span class="tag tag-coral">Aguardando</span></div>
      <div class="os-items">🍤 Camarão grelhado · 🍺 Cerveja (2)</div>
      <div class="os-footer">
        <div class="os-token">Token: <strong>4827</strong> · 11h–12h</div>
        <div class="os-total">R$ 67,50</div>
      </div>
    </div>
    <div class="order-status-card">
      <div class="os-header"><div class="os-kiosk">Barraca do Sol</div><span class="tag tag-success">Concluído ✓</span></div>
      <div class="os-items">🌮 Combo petisco (1) · 🥤 Suco (2)</div>
      <div class="os-footer">
        <div class="os-token">Token: <strong>1234</strong> · 13h–14h</div>
        <div class="os-total" style="color:var(--success)">R$ 38,70 ✓</div>
      </div>
    </div>
  </div>
  <nav class="bottom-nav">
    <button class="nav-btn" onclick="go('s-home')"><span class="ni">🏠</span>Início</button>
    <button class="nav-btn active"><span class="ni">📋</span>Pedidos</button>
    <button class="nav-btn" onclick="go('s-wallet')"><span class="ni">💳</span>Carteira</button>
    <button class="nav-btn" onclick="openModal('modal-profile')"><span class="ni">👤</span>Perfil</button>
  </nav>
</div>

<!-- ══ MODAIS ══ -->
<div class="modal" id="modal-recharge" onclick="closeModal('modal-recharge')">
  <div class="modal-box" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal('modal-recharge')">✕</button>
    <div class="modal-title">💰 Adicionar saldo</div>
    <div class="input-group"><label>Valor</label><input type="number" placeholder="R$ 0,00" id="recharge-val" style="font-size:22px;font-weight:700"></div>
    <div style="display:flex;gap:8px;margin-bottom:14px">
      <button onclick="document.getElementById('recharge-val').value=50" style="flex:1;padding:9px;border-radius:10px;border:2px solid var(--sand);background:white;font-weight:700;cursor:pointer">R$ 50</button>
      <button onclick="document.getElementById('recharge-val').value=100" style="flex:1;padding:9px;border-radius:10px;border:2px solid var(--sand);background:white;font-weight:700;cursor:pointer">R$ 100</button>
      <button onclick="document.getElementById('recharge-val').value=200" style="flex:1;padding:9px;border-radius:10px;border:2px solid var(--sand);background:white;font-weight:700;cursor:pointer">R$ 200</button>
    </div>
    <button class="btn btn-primary" onclick="closeModal('modal-recharge');alert('✅ Pix gerado! Escaneie o QR Code no seu banco.')">⚡ Pagar via Pix</button>
    <button class="btn btn-ocean" style="margin-top:8px" onclick="closeModal('modal-recharge')">💳 Cartão de crédito</button>
  </div>
</div>

<div class="modal" id="modal-antecip" onclick="closeModal('modal-antecip')">
  <div class="modal-box" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal('modal-antecip')">✕</button>
    <div class="modal-title">⚡ Confirmar antecipação</div>
    <div style="padding:14px;background:var(--cream);border-radius:var(--radius-sm);margin-bottom:14px">
      <div style="display:flex;justify-content:space-between;font-size:14px;padding:4px 0"><span>Valor bruto</span><span style="font-weight:700">R$ 405,00</span></div>
      <div style="display:flex;justify-content:space-between;font-size:14px;padding:4px 0;color:var(--coral)"><span>Taxa (13%)</span><span>- R$ 52,65</span></div>
      <div style="border-top:2px solid var(--sand);margin-top:8px;padding-top:8px;display:flex;justify-content:space-between"><span style="font-weight:700">Você recebe</span><span style="font-weight:800;color:var(--ocean);font-size:18px">R$ 352,35</span></div>
    </div>
    <div class="input-group"><label>Chave Pix</label><input type="text" placeholder="CNPJ ou chave Pix"></div>
    <button class="btn btn-primary" onclick="closeModal('modal-antecip');alert('✅ Antecipação solicitada! Pix em instantes.')">Confirmar antecipação</button>
  </div>
</div>

<div class="modal" id="modal-share" onclick="closeModal('modal-share')">
  <div class="modal-box" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal('modal-share')">✕</button>
    <div class="modal-title">📤 Compartilhar token</div>
    <p style="font-size:13px;color:var(--mid);margin-bottom:14px">Envie seu token para outra pessoa resgatar no quiosque</p>
    <button class="btn btn-success" onclick="closeModal('modal-share')">📱 WhatsApp</button>
    <button class="btn btn-ocean" style="margin-top:8px" onclick="closeModal('modal-share')">📋 Copiar token</button>
    <button class="btn btn-outline" style="margin-top:8px" onclick="closeModal('modal-share')">✉️ E-mail</button>
  </div>
</div>

<div class="modal" id="modal-profile" onclick="closeModal('modal-profile')">
  <div class="modal-box" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal('modal-profile')">✕</button>
    <div class="modal-title">👤 Meu Perfil</div>
    <div style="text-align:center;padding:10px 0 20px">
      <div style="width:70px;height:70px;border-radius:50%;background:var(--ocean);display:flex;align-items:center;justify-content:center;font-size:30px;margin:0 auto 10px">👤</div>
      <div style="font-family:'Syne',sans-serif;font-weight:700;font-size:18px">Marcelo Boghi</div>
      <div style="font-size:13px;color:var(--mid)">CPF: •••.469.•••-40</div>
    </div>
    <div class="input-group"><label>E-mail</label><input type="email" value="marcelo.boghi@gmail.com"></div>
    <div class="input-group"><label>Telefone</label><input type="tel" placeholder="(00) 00000-0000"></div>
    <button class="btn btn-ocean" onclick="closeModal('modal-profile')">Salvar alterações</button>
    <button class="btn btn-outline" style="margin-top:8px;color:var(--danger);border-color:var(--danger)" onclick="go('s-splash')">Sair da conta</button>
  </div>
</div>

<div class="modal" id="modal-settings" onclick="closeModal('modal-settings')">
  <div class="modal-box" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal('modal-settings')">✕</button>
    <div class="modal-title">⚙️ Configurações do Quiosque</div>
    <div class="input-group"><label>Nome do quiosque</label><input type="text" value="Quiosque Maresias"></div>
    <div class="input-group"><label>Telefone de contato</label><input type="tel" placeholder="(00) 00000-0000"></div>
    <div class="input-group"><label>Horário de abertura</label><input type="time" value="09:00"></div>
    <div class="input-group"><label>Horário de fechamento</label><input type="time" value="18:00"></div>
    <button class="btn btn-ocean" onclick="closeModal('modal-settings')">Salvar configurações</button>
  </div>
</div>

<div class="modal" id="modal-orders-preview" onclick="closeModal('modal-orders-preview')">
  <div class="modal-box" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal('modal-orders-preview')">✕</button>
    <div class="modal-title">📋 Meus Pedidos</div>
    <div class="order-status-card">
      <div class="os-header"><div class="os-kiosk">Quiosque Maresias</div><span class="tag tag-coral">Aguardando</span></div>
      <div class="os-items">🍤 Camarão grelhado · 🍺 Cerveja (2)</div>
      <div class="os-footer">
        <div class="os-token">Token: <strong>4827</strong></div>
        <div class="os-total">R$ 67,50</div>
      </div>
    </div>
    <button class="btn btn-ocean" onclick="go('s-orders');closeModal('modal-orders-preview')">Ver todos os pedidos</button>
  </div>
</div>

<script>
// ── DATA ──────────────────────────────────────────────────
const MENU = [
  {id:1,name:'Camarão grelhado',desc:'300g · arroz e farofa',emoji:'🍤',cat:'comida',price:45},
  {id:2,name:'Peixe frito',desc:'Filé de tilápia crocante',emoji:'🐟',cat:'comida',price:38},
  {id:3,name:'Combo petisco',desc:'Bolinhos, frango e mandioca',emoji:'🌮',cat:'petisco',price:28},
  {id:4,name:'Isca de frango',desc:'Com molho especial da casa',emoji:'🍗',cat:'petisco',price:22},
  {id:5,name:'Cerveja gelada',desc:'Long neck 355ml',emoji:'🍺',cat:'bebida',price:12},
  {id:6,name:'Suco natural',desc:'Laranja, limão ou maracujá',emoji:'🥤',cat:'bebida',price:14},
  {id:7,name:'Água de coco',desc:'Gelada na própria coco',emoji:'🥥',cat:'bebida',price:16},
  {id:8,name:'Refrigerante',desc:'Lata 350ml',emoji:'🥫',cat:'bebida',price:8},
];
const DISCOUNT = 0.10, FEE = 0.03;
let cart = {}, selTime = '11h–12h', payMethod = 'saldo', loginType = 'cliente';

// ── NAV ──────────────────────────────────────────────────
function go(id, type) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  window.scrollTo(0,0);
  if(type) loginType = type;
  if(id==='s-login') setupLogin();
  if(id==='s-checkout') renderCheckout();
  if(id==='s-token') updateToken();
  if(id==='s-painel') setupPainel();
  if(id==='s-cadastro') initCadastro();
}
function openModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

function setupLogin() {
  const isEstab = loginType === 'estab';
  document.getElementById('login-title').textContent = isEstab ? 'Área do Estabelecimento 🏪' : 'Bem-vindo! 👋';
  document.getElementById('login-sub').textContent = isEstab ? 'Entre com CNPJ ou e-mail' : 'Entre com CPF ou e-mail';
}
function doLogin() {
  if(loginType === 'estab') go('s-painel');
  else go('s-home');
}
function loginTab(btn, tab) {
  document.querySelectorAll('.login-tab').forEach(t => t.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('tab-login').style.display = tab==='tab-login'?'block':'none';
  document.getElementById('tab-cadastro').style.display = tab==='tab-cadastro'?'block':'none';
}

// ── MENU ─────────────────────────────────────────────────
function renderMenu(cat='all') {
  const items = cat==='all' ? MENU : MENU.filter(i=>i.cat===cat);
  document.getElementById('menu-items').innerHTML = items.map(item => {
    const disc = (item.price*(1-DISCOUNT)).toFixed(2).replace('.',',');
    const orig = item.price.toFixed(2).replace('.',',');
    const qty = cart[item.id]||0;
    return `<div class="menu-item">
      <div class="item-emoji">${item.emoji}</div>
      <div class="item-info">
        <div class="item-name">${item.name}</div>
        <div class="item-desc">${item.desc}</div>
        <div class="item-prices">
          <span class="item-original">R$ ${orig}</span>
          <span class="item-price">R$ ${disc}</span>
          <span class="tag tag-lime" style="font-size:10px">-10%</span>
        </div>
      </div>
      <div>${qty===0
        ? `<button class="item-add-btn" onclick="addItem(${item.id})">+</button>`
        : `<div class="item-qty">
            <button class="qty-btn qty-minus" onclick="chgQty(${item.id},-1)">−</button>
            <span class="qty-num">${qty}</span>
            <button class="qty-btn qty-plus" onclick="chgQty(${item.id},1)">+</button>
           </div>`
      }</div>
    </div>`;
  }).join('');
}
function addItem(id) { cart[id]=1; updateCart(); renderMenu(getCat()); }
function chgQty(id,d) { cart[id]=(cart[id]||0)+d; if(cart[id]<=0) delete cart[id]; updateCart(); renderMenu(getCat()); }
function getCat() {
  const a = document.querySelector('.cat-btn.active');
  if(!a) return 'all';
  const t = a.textContent;
  if(t.includes('Todos')) return 'all';
  if(t.includes('Comida')) return 'comida';
  if(t.includes('Bebidas')) return 'bebida';
  return 'petisco';
}
function updateCart() {
  const qty = Object.values(cart).reduce((a,b)=>a+b,0);
  const sub = Object.entries(cart).reduce((a,[id,q])=>{
    const it=MENU.find(i=>i.id==id); return a+(it?it.price*q:0);
  },0);
  const total = sub*(1-DISCOUNT);
  document.getElementById('cart-badge').textContent = qty;
  document.getElementById('cart-total').textContent = 'R$ '+total.toFixed(2).replace('.',',');
  document.getElementById('cart-bar').classList.toggle('visible', qty>0);
  window._cartTotal = total;
}
function filterCat(btn, cat) {
  document.querySelectorAll('.cat-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderMenu(cat);
}
function selectTime(el, t) {
  document.querySelectorAll('.time-slot').forEach(s=>s.classList.remove('active'));
  el.classList.add('active');
  selTime = t;
}
function switchView(v) {
  document.getElementById('btn-list').classList.toggle('active', v==='list');
  document.getElementById('btn-map').classList.toggle('active', v==='map');
  document.getElementById('view-list').style.display = v==='list'?'flex':'none';
  document.getElementById('view-map').classList.toggle('active', v==='map');
}

// ── CHECKOUT ─────────────────────────────────────────────
function renderCheckout() {
  const entries = Object.entries(cart);
  if(!entries.length) return;
  document.getElementById('checkout-time').textContent = selTime;
  document.getElementById('checkout-items').innerHTML = entries.map(([id,qty])=>{
    const it=MENU.find(i=>i.id==id);
    const p=(it.price*(1-DISCOUNT)*qty).toFixed(2).replace('.',',');
    return `<div class="order-line">
      <div><div class="name">${it.emoji} ${it.name}</div><div class="qty-label">${qty}x · R$ ${(it.price*(1-DISCOUNT)).toFixed(2).replace('.',',')} cada</div></div>
      <div class="price">R$ ${p}</div>
    </div>`;
  }).join('');
  const sub = entries.reduce((a,[id,q])=>{ const it=MENU.find(i=>i.id==id); return a+it.price*q; },0);
  const disc = sub*DISCOUNT;
  const after = sub-disc;
  const fee = after*FEE;
  const creditFee = payMethod==='credito' ? after*0.038 : 0;
  const total = after+creditFee;
  window._checkoutTotal = total;
  document.getElementById('price-breakdown').innerHTML = `
    <div class="price-row"><span>Subtotal</span><span>R$ ${sub.toFixed(2).replace('.',',')}</span></div>
    <div class="price-row discount"><span>🎉 Desconto antecipado (10%)</span><span>- R$ ${disc.toFixed(2).replace('.',',')}</span></div>
    ${creditFee>0?`<div class="price-row fee"><span>💳 Taxa Mercado Pago (~3,8%)</span><span>R$ ${creditFee.toFixed(2).replace('.',',')}</span></div>`:''}
    <div class="price-row fee"><span>Taxa de serviço (3%)</span><span>R$ ${fee.toFixed(2).replace('.',',')}</span></div>
    <div class="price-row total"><span>Total</span><span>R$ ${total.toFixed(2).replace('.',',')}</span></div>`;
}
function selectPay(el, m) {
  document.querySelectorAll('.pay-method').forEach(p=>p.classList.remove('active'));
  el.classList.add('active');
  payMethod = m;
  const notes = {saldo:'✅ Sem taxa adicional ao usar Saldo PedeFácil',pix:'⚡ Sem taxa adicional no Pix',credito:'💳 Taxa do Mercado Pago (~3,8%) será aplicada'};
  document.getElementById('pay-note').textContent = notes[m];
  renderCheckout();
}
function updateToken() {
  document.getElementById('token-display').textContent = Math.floor(1000+Math.random()*9000);
  document.getElementById('token-time').textContent = selTime;
  document.getElementById('token-total').textContent = 'R$ '+(window._checkoutTotal||0).toFixed(2).replace('.',',');
}

// ── PAINEL ───────────────────────────────────────────────
function painelTab(btn, tab) {
  document.querySelectorAll('.painel-tab').forEach(t=>t.classList.remove('active'));
  document.querySelectorAll('.painel-section').forEach(s=>s.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById(tab).classList.add('active');
}
function setupPainel() {
  const days = ['domingo','segunda-feira','terça-feira','quarta-feira','quinta-feira','sexta-feira','sábado'];
  const months = ['janeiro','fevereiro','março','abril','maio','junho','julho','agosto','setembro','outubro','novembro','dezembro'];
  const now = new Date();
  document.getElementById('painel-date').textContent = `${days[now.getDay()]}, ${now.getDate()} de ${months[now.getMonth()]}`;
}
function validateOrder(n, token) {
  document.getElementById('ob-'+n).className='tag tag-success';
  document.getElementById('ob-'+n).textContent='Validado ✓';
  const btn = document.getElementById('vb-'+n);
  btn.className='validate-btn validated'; btn.disabled=true;
  btn.textContent='✅ Preparo iniciado · Crédito liberado';
  const p=parseInt(document.getElementById('pendentes-count').textContent)-1;
  const v=parseInt(document.getElementById('validados-count').textContent)+1;
  document.getElementById('pendentes-count').textContent=p;
  document.getElementById('validados-count').textContent=v;
}
function validateToken() {
  const val = document.getElementById('token-val-input').value.trim();
  if(val==='4827'){validateOrder(1,'4827');alert('✅ Token 4827 validado! Camarão em preparo. Crédito liberado!');}
  else if(val==='3591'){validateOrder(2,'3591');alert('✅ Token 3591 validado! Pedido da Maria em preparo!');}
  else if(val){alert('❌ Token não encontrado. Verifique com o cliente.');}
  document.getElementById('token-val-input').value='';
}
function toggleDiscount(el) {
  const msg = el.checked ? '✅ Desconto de 10% ativado! Clientes verão o badge "10% OFF".' : '⚠️ Desconto desativado. Clientes verão preços normais.';
  alert(msg);
}

// ── CADASTRO ─────────────────────────────────────────────
let currentStep = 1;
const totalSteps = 6;
const stepLabels = ['Dados da Empresa','Responsável Legal','Endereço','Quadro de Sócios','Dados Bancários','Documentos'];
let socioCount = 1;

function initCadastro() {
  currentStep = 1;
  updateStep();
  const dots = document.getElementById('step-dots');
  dots.innerHTML = Array.from({length:totalSteps},(_,i)=>`<div class="section-dot ${i===0?'active':''}" onclick="goStep(${i+1})" id="dot-${i+1}"></div>`).join('');
}
function updateStep() {
  document.querySelectorAll('.form-section').forEach(s=>s.classList.remove('active'));
  document.getElementById('fs-'+currentStep).classList.add('active');
  const pct = Math.round((currentStep/totalSteps)*100);
  document.getElementById('prog-fill').style.width = pct+'%';
  document.getElementById('step-label').textContent = `Passo ${currentStep} de ${totalSteps} — ${stepLabels[currentStep-1]}`;
  document.getElementById('step-pct').textContent = pct+'%';
  document.getElementById('btn-prev').style.display = currentStep>1?'block':'none';
  document.getElementById('btn-next').style.display = currentStep<totalSteps?'block':'none';
  for(let i=1;i<=totalSteps;i++){
    const d=document.getElementById('dot-'+i);
    if(d){ d.className='section-dot'+(i===currentStep?' active':i<currentStep?' done':''); }
  }
}
function nextStep() { if(currentStep<totalSteps){currentStep++;updateStep();} }
function prevStep() { if(currentStep>1){currentStep--;updateStep();} }
function goStep(n) { currentStep=n; updateStep(); }
function addSocio() {
  socioCount++;
  const div=document.createElement('div');
  div.className='socio-card';
  div.id='socio-'+socioCount;
  div.innerHTML=`<div style="font-size:12px;font-weight:700;color:var(--ocean);margin-bottom:8px">Sócio ${socioCount}</div>
    <button class="socio-remove" onclick="removeSocio(${socioCount})">✕</button>
    <div class="input-group"><label>Nome</label><input type="text" placeholder="Nome completo"></div>
    <div style="display:flex;gap:8px">
      <div class="input-group" style="flex:2"><label>CPF</label><input type="text" placeholder="000.000.000-00"></div>
      <div class="input-group" style="flex:1"><label>Participação</label><input type="text" placeholder="%"></div>
    </div>
    <div class="input-group"><label>Cargo</label><input type="text" placeholder="Cargo"></div>`;
  document.getElementById('socios-list').appendChild(div);
}
function removeSocio(n) { const el=document.getElementById('socio-'+n); if(el)el.remove(); }
function submitCadastro() { alert('✅ Cadastro enviado com sucesso!\n\nNossa equipe analisará seus documentos em até 2 dias úteis.\nVocê receberá uma notificação por e-mail.'); go('s-painel'); }
function markUploaded(btn, name) { btn.classList.add('uploaded'); btn.innerHTML='✅ '+name+' — Enviado'; }

// ── UTILS ─────────────────────────────────────────────────
function maskCNPJ(el) {
  let v=el.value.replace(/\D/g,'').substring(0,14);
  if(v.length>12) v=v.replace(/^(\d{2})(\d{3})(\d{3})(\d{4})(\d{2})$/,'$1.$2.$3/$4-$5');
  else if(v.length>8) v=v.replace(/^(\d{2})(\d{3})(\d{3})(\d{4})/,'$1.$2.$3/$4');
  else if(v.length>5) v=v.replace(/^(\d{2})(\d{3})(\d{3})/,'$1.$2.$3');
  else if(v.length>2) v=v.replace(/^(\d{2})(\d{3})/,'$1.$2');
  el.value=v;
}
function maskCEP(el) {
  let v=el.value.replace(/\D/g,'').substring(0,8);
  if(v.length>5) v=v.replace(/^(\d{5})(\d)/,'$1-$2');
  el.value=v;
}
function buscarCEP() { alert('🔍 Buscando CEP...\n(Integração com ViaCEP será ativada na versão de produção)'); }
function updatePixPlaceholder() {
  const t=document.getElementById('pix-type').value;
  const p={cpf:'000.000.000-00',cnpj:'00.000.000/0000-00',email:'chave@email.com',tel:'(00) 00000-0000',random:'Chave aleatória de 32 caracteres'};
  document.getElementById('pix-key').placeholder=p[t]||'';
}

// ── INIT ─────────────────────────────────────────────────
renderMenu();
document.getElementById('view-list').style.display='flex';
document.getElementById('view-list').style.flexDirection='column';
</script>
</body>
</html># pedefacil
