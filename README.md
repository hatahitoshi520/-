# -<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>☕ 喫茶すず</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
:root{
  --br:#6B3F1E;--bl:#C8956C;--cream:#FBF6EC;--dark:#3B2213;
  --cb:rgba(107,63,30,0.13);--cbm:rgba(107,63,30,0.25);
  --bg:#F7F2EA;--surface:#fff;--text:#1A1008;--text2:#6B5744;--text3:#A8937E;
  --green:#3B6D11;--greenBg:#EAF3DE;--red:#C0392B;--redBg:#FDECEA;
  --blue:#185FA5;--blueBg:#E6F1FB;
}
html,body{min-height:100%;background:var(--bg);font-family:-apple-system,BlinkMacSystemFont,'Hiragino Kaku Gothic ProN','Hiragino Sans',YuGothic,sans-serif;color:var(--text);font-size:15px;}
.app{max-width:430px;margin:0 auto;padding-bottom:96px;}

/* ヘッダー */
.header{background:var(--br);color:var(--cream);padding:1rem 1.25rem .8rem;border-radius:0 0 16px 16px;margin-bottom:1rem;position:sticky;top:0;z-index:50;}
.hrow{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:.45rem;}
.htitle{font-size:16px;font-weight:600;letter-spacing:.04em;}
.hdate{font-size:11px;opacity:.65;margin-top:2px;}
.hright{text-align:right;}
.hnum{font-size:21px;font-weight:700;line-height:1;}
.hlbl{font-size:10px;opacity:.6;margin-top:2px;}
.pbar-wrap{background:rgba(255,255,255,.18);border-radius:3px;height:4px;margin-top:.5rem;}
.pbar-fill{height:4px;border-radius:3px;background:var(--cream);transition:width .35s;}
.pbar-row{display:flex;justify-content:space-between;font-size:10px;opacity:.5;margin-top:3px;}

/* 曜日タブ */
.dtabs{display:flex;overflow-x:auto;gap:6px;padding:0 1rem;margin-bottom:.9rem;scrollbar-width:none;}
.dtabs::-webkit-scrollbar{display:none;}
.dtab{flex-shrink:0;padding:6px 14px;border-radius:20px;border:1px solid var(--cbm);background:var(--surface);color:var(--text2);font-size:13px;cursor:pointer;white-space:nowrap;font-weight:500;}
.dtab.active{background:var(--br);color:var(--cream);border-color:var(--br);}
.dtab.today-mark{border-color:var(--bl);}

/* セクション */
.sec{padding:0 1rem;margin-bottom:1rem;}
.sec-lbl{font-size:10px;font-weight:600;letter-spacing:.08em;color:var(--bl);text-transform:uppercase;margin-bottom:.4rem;}
.card{background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;box-shadow:0 1px 3px rgba(107,63,30,.06);}

/* タスク行 */
.trow{display:flex;align-items:flex-start;gap:11px;padding:11px 14px;border-bottom:.5px solid var(--cb);cursor:pointer;transition:background .1s;}
.trow:last-child{border-bottom:none;}
.trow:active{background:var(--cream);}
.trow.done .tlbl{text-decoration:line-through;color:var(--text3);}
.tchk{width:21px;height:21px;border-radius:50%;border:1.5px solid var(--cbm);display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px;transition:all .15s;}
.trow.done .tchk{background:var(--br);border-color:var(--br);}
.chk-icon{display:none;width:12px;height:12px;stroke:#fff;stroke-width:2.5;fill:none;}
.trow.done .chk-icon{display:block;}
.tinfo{flex:1;min-width:0;}
.tlbl{font-size:13px;color:var(--text);line-height:1.4;}
.tnote{font-size:11px;color:var(--text3);margin-top:2px;}
.tbadge{font-size:10px;padding:2px 7px;border-radius:8px;font-weight:600;flex-shrink:0;margin-top:2px;}
.b-op{background:var(--cream);color:var(--br);border:.5px solid var(--bl);}
.b-cl{background:var(--dark);color:var(--bl);}
.b-dy{background:#F0EBE3;color:var(--text2);}
.b-cl2{background:var(--greenBg);color:var(--green);}

/* タスク完了送信ボタン */
.task-submit-area{padding:0 1rem;margin-bottom:.5rem;}
.task-submit-btn{width:100%;padding:13px;background:var(--green);color:#fff;border:none;border-radius:12px;font-size:14px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px;letter-spacing:.04em;}
.task-submit-btn:active{opacity:.85;}
.task-submit-btn:disabled{opacity:.4;cursor:default;}

/* 買い出し */
.bcat-hd{display:flex;font-size:10px;color:var(--text3);padding:7px 14px 5px;border-bottom:.5px solid var(--cb);font-weight:600;letter-spacing:.04em;}
.bcat-hd-name{flex:1;}
.bcat-hd-stock{width:68px;text-align:center;}
.bcat-hd-need{width:90px;text-align:center;}
.brow{display:flex;align-items:center;padding:10px 14px;border-bottom:.5px solid var(--cb);transition:background .1s;}
.brow:last-child{border-bottom:none;}
.brow.bought{background:#F8FBF4;}
.bchk{width:22px;height:22px;border-radius:6px;border:1.5px solid var(--cbm);display:flex;align-items:center;justify-content:center;flex-shrink:0;cursor:pointer;transition:all .15s;margin-right:10px;}
.brow.bought .bchk{background:var(--br);border-color:var(--br);}
.binfo{flex:1;min-width:0;}
.bname{font-size:13px;color:var(--text);line-height:1.35;}
.brow.bought .bname{text-decoration:line-through;color:var(--text3);}
.blow-tag{font-size:10px;background:var(--redBg);color:var(--red);border-radius:5px;padding:1px 5px;margin-left:4px;font-weight:600;}
.bstock{width:68px;text-align:center;flex-shrink:0;}
.bstock-val{font-size:11px;color:var(--text3);background:var(--bg);border-radius:6px;padding:3px 5px;display:inline-block;}
.bneed{width:90px;flex-shrink:0;display:flex;align-items:center;justify-content:center;gap:3px;}
.bneed-btn{width:26px;height:26px;border-radius:7px;border:1px solid var(--cbm);background:var(--surface);color:var(--br);font-size:16px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:background .1s;flex-shrink:0;line-height:1;}
.bneed-btn:active{background:var(--cream);}
.bneed-val{font-size:14px;font-weight:700;color:var(--br);min-width:18px;text-align:center;}
.bneed-val.zero{color:var(--text3);font-weight:400;}
.buy-summary{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;}
.buy-sum-lbl{font-size:12px;color:var(--text2);}
.buy-sum-num{font-size:13px;font-weight:700;color:var(--br);}
.send-area{padding:0 1rem;margin-bottom:.5rem;}
.send-btn{width:100%;padding:12px;background:var(--br);color:var(--cream);border:none;border-radius:10px;font-size:14px;font-weight:600;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px;}
.send-btn:active{opacity:.85;}
.send-btn:disabled{opacity:.4;cursor:default;}

/* 日次固定情報バナー */
.daily-info-banner{margin:0 1rem 1rem;background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;box-shadow:0 1px 3px rgba(107,63,30,.06);}
.daily-info-header{display:flex;align-items:center;justify-content:space-between;padding:10px 14px 6px;}
.daily-info-lbl{font-size:10px;font-weight:700;letter-spacing:.08em;color:var(--bl);text-transform:uppercase;}
.daily-info-edit{font-size:11px;color:var(--br);cursor:pointer;padding:3px 8px;border:.5px solid var(--bl);border-radius:8px;background:var(--cream);}
.daily-info-row{display:flex;align-items:center;gap:8px;padding:0 14px 10px;flex-wrap:wrap;}
.daily-info-chip{display:flex;align-items:center;gap:5px;background:var(--cream);border:.5px solid var(--cbm);border-radius:20px;padding:4px 10px;font-size:13px;font-weight:600;color:var(--text);}
.daily-info-chip span{font-size:11px;color:var(--text3);font-weight:400;}
.daily-info-empty{padding:0 14px 10px;font-size:12px;color:var(--text3);}
.daily-info-edit-area{display:none;padding:0 14px 12px;border-top:.5px solid var(--cb);margin-top:6px;}
.daily-info-edit-area.open{display:block;}
.daily-info-edit-area .field-lbl{font-size:11px;color:var(--text3);display:block;margin-bottom:4px;margin-top:10px;}
.daily-info-edit-area input{width:100%;padding:9px 10px;font-size:14px;border:.5px solid var(--cbm);border-radius:8px;color:var(--text);background:var(--bg);font-family:inherit;outline:none;}
.daily-info-edit-area input:focus{border-color:var(--br);}
.weather-radio{display:flex;gap:6px;margin-top:4px;}
.weather-radio-btn{flex:1;padding:8px 4px;text-align:center;font-size:13px;font-weight:600;border-radius:9px;border:1.5px solid var(--cbm);background:var(--surface);color:var(--text2);cursor:pointer;}
.weather-radio-btn.active{background:var(--br);color:var(--cream);border-color:var(--br);}
.daily-save-btn{width:100%;margin-top:12px;padding:10px;background:var(--br);color:var(--cream);border:none;border-radius:9px;font-size:13px;font-weight:700;cursor:pointer;}
.daily-save-btn:active{opacity:.85;}

/* 日報・会計フォーム */
.rep-header{background:var(--br);color:var(--cream);padding:1rem 1.25rem .8rem;margin-bottom:1rem;}
.rep-header-title{font-size:16px;font-weight:600;}
.rep-header-sub{font-size:11px;opacity:.7;margin-top:3px;}
.form-row{padding:0 1rem;margin-bottom:.9rem;}
.form-lbl{font-size:10px;font-weight:700;letter-spacing:.08em;color:var(--bl);text-transform:uppercase;margin-bottom:.4rem;}
.form-card{background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;box-shadow:0 1px 3px rgba(107,63,30,.06);}
.field-wrap{padding:0 14px;}
.field-lbl{font-size:11px;color:var(--text3);padding-top:8px;display:block;}
.field-input{width:100%;padding:8px 0 10px;font-size:15px;border:none;border-bottom:.5px solid var(--cb);color:var(--text);background:transparent;font-family:inherit;outline:none;}
.field-input:last-child{border-bottom:none;}
.field-input:focus{background:var(--cream);}
textarea.field-input{resize:none;line-height:1.5;padding-top:8px;}
.radio-group{display:flex;gap:6px;padding:10px 14px;flex-wrap:wrap;}
.radio-btn{flex:1;min-width:55px;padding:9px 6px;text-align:center;font-size:13px;font-weight:600;border-radius:9px;border:1.5px solid var(--cbm);background:var(--surface);color:var(--text2);cursor:pointer;}
.radio-btn.active{background:var(--br);color:var(--cream);border-color:var(--br);}
.num-row{display:flex;align-items:center;gap:10px;padding:10px 14px;}
.num-btn{width:38px;height:38px;border-radius:10px;border:1.5px solid var(--cbm);background:var(--surface);color:var(--text);font-size:18px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;}
.num-btn:active{background:var(--cream);}
.num-val{font-size:22px;font-weight:700;color:var(--br);min-width:30px;text-align:center;}

/* メニュー選択 */
.menu-cat-hd{display:flex;align-items:center;justify-content:space-between;padding:9px 14px;background:var(--br);color:var(--cream);cursor:pointer;font-size:13px;font-weight:700;}
.menu-cat-hd .badge{font-size:11px;background:var(--bl);color:var(--dark);padding:1px 7px;border-radius:8px;font-weight:700;}
.menu-items{display:none;background:var(--surface);}
.menu-items.open{display:block;}
.menu-item-row{display:flex;align-items:center;justify-content:space-between;padding:9px 14px;border-bottom:.5px solid var(--cb);}
.menu-item-row:last-child{border-bottom:none;}
.menu-item-name{font-size:13px;color:var(--text);}
.menu-item-price{font-size:12px;color:var(--text3);margin-top:1px;}
.menu-item-qty{display:flex;align-items:center;gap:6px;}
.mq-btn{width:30px;height:30px;border-radius:8px;border:1px solid var(--cbm);background:var(--surface);color:var(--br);font-size:18px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;line-height:1;}
.mq-btn.plus{background:var(--br);border-color:var(--br);color:var(--cream);}
.mq-btn:active{opacity:.75;}
.mq-num{font-size:16px;font-weight:700;min-width:20px;text-align:center;color:#ccc;}
.mq-num.on{color:var(--br);}

/* 合計パネル */
.total-panel{background:var(--dark);border-radius:12px;padding:14px;margin:0 1rem 1rem;}
.total-row{display:flex;justify-content:space-between;font-size:13px;color:var(--bl);margin-bottom:5px;}
.total-grand{display:flex;justify-content:space-between;font-size:24px;font-weight:700;color:var(--cream);border-top:1px solid #5c3a1e;padding-top:10px;margin-top:6px;}

/* 送信ボタン系 */
.submit-btn{width:calc(100% - 2rem);margin:0 1rem .5rem;padding:14px;background:var(--br);color:var(--cream);border:none;border-radius:12px;font-size:15px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;letter-spacing:.04em;}
.submit-btn:active{opacity:.85;}
.submit-btn:disabled{opacity:.4;cursor:default;}
.reset-btn{width:calc(100% - 2rem);margin:0 1rem .5rem;padding:9px;background:none;border:.5px solid var(--cbm);border-radius:8px;color:var(--text3);font-size:12px;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:5px;}
.reset-btn:active{background:var(--cream);}
.msg-box{margin:0 1rem .5rem;padding:12px;border-radius:10px;font-size:13px;font-weight:600;text-align:center;display:none;white-space:pre-line;}
.msg-ok{background:var(--greenBg);color:var(--green);}
.msg-err{background:var(--redBg);color:var(--red);}
.msg-load{background:var(--cream);color:var(--text2);}

/* 会計履歴 */
.hist-header{display:flex;align-items:center;justify-content:space-between;padding:0 1rem;margin-bottom:.5rem;}
.hist-title{font-size:13px;font-weight:700;color:var(--text2);}
.hist-sum{font-size:13px;font-weight:700;color:var(--br);}
.hist-card{background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;margin:0 1rem 1rem;box-shadow:0 1px 3px rgba(107,63,30,.06);}
.hist-empty{padding:20px;text-align:center;color:var(--text3);font-size:13px;}
.hist-row{display:flex;align-items:flex-start;padding:11px 14px;border-bottom:.5px solid var(--cb);gap:10px;position:relative;}
.hist-row:last-child{border-bottom:none;}
.hist-time{font-size:11px;color:var(--text3);flex-shrink:0;margin-top:2px;min-width:72px;}
.hist-info{flex:1;min-width:0;}
.hist-tbl{font-size:12px;color:var(--text2);margin-bottom:2px;}
.hist-order{font-size:11px;color:var(--text3);line-height:1.4;}
.hist-amt{font-size:16px;font-weight:700;color:var(--br);flex-shrink:0;text-align:right;}
.hist-staff{font-size:10px;color:var(--text3);text-align:right;margin-top:2px;}
/* 削除ボタン */
.hist-del-btn{position:absolute;top:8px;right:8px;width:22px;height:22px;border-radius:50%;background:var(--redBg);border:none;color:var(--red);font-size:14px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;line-height:1;opacity:0;transition:opacity .15s;}
.hist-row:hover .hist-del-btn{opacity:1;}
.hist-row .hist-del-btn{opacity:.35;}
.hist-del-btn:active{opacity:1;background:var(--red);color:#fff;}
.day-total-bar{background:var(--cream);border:.5px solid var(--cb);border-radius:10px;padding:10px 14px;margin:0 1rem .6rem;display:flex;justify-content:space-between;align-items:center;}
.day-total-lbl{font-size:12px;color:var(--text2);}
.day-total-val{font-size:18px;font-weight:700;color:var(--br);}
.day-count{font-size:11px;color:var(--text3);}

/* 日付フィルタ */
.date-filter{display:flex;overflow-x:auto;gap:6px;padding:0 1rem;margin-bottom:.8rem;scrollbar-width:none;}
.date-filter::-webkit-scrollbar{display:none;}
.date-tab{flex-shrink:0;padding:5px 12px;border-radius:16px;border:1px solid var(--cbm);background:var(--surface);color:var(--text2);font-size:12px;cursor:pointer;white-space:nowrap;}
.date-tab.active{background:var(--br);color:var(--cream);border-color:var(--br);}

/* ===== 経費・支出管理 ===== */
.exp-cat-badge{font-size:10px;padding:2px 7px;border-radius:8px;font-weight:600;}
.exp-food{background:#FFF5E0;color:#B87333;}
.exp-util{background:#E8F4FD;color:#1A5C8A;}
.exp-supply{background:var(--greenBg);color:var(--green);}
.exp-other{background:#F0EBE3;color:var(--text2);}
.exp-row{display:flex;align-items:flex-start;padding:11px 14px;border-bottom:.5px solid var(--cb);gap:10px;position:relative;}
.exp-row:last-child{border-bottom:none;}
.exp-del-btn{width:22px;height:22px;border-radius:50%;background:var(--redBg);border:none;color:var(--red);font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;line-height:1;margin-top:1px;}
.exp-del-btn:active{background:var(--red);color:#fff;}
.exp-info{flex:1;min-width:0;}
.exp-name{font-size:13px;color:var(--text);}
.exp-meta{font-size:11px;color:var(--text3);margin-top:2px;}
.exp-amt{font-size:15px;font-weight:700;color:var(--red);flex-shrink:0;text-align:right;}
/* 確定申告サマリ */
.tax-panel{background:var(--dark);border-radius:12px;padding:14px;margin:0 1rem 1rem;}
.tax-row{display:flex;justify-content:space-between;font-size:13px;color:var(--bl);margin-bottom:7px;align-items:center;}
.tax-row:last-child{margin-bottom:0;}
.tax-lbl{color:var(--bl);}
.tax-val{font-size:15px;font-weight:700;color:var(--cream);}
.tax-profit{font-size:20px;font-weight:700;color:#7FE0A0;}
.tax-section-hd{font-size:10px;font-weight:700;letter-spacing:.08em;color:var(--bl);text-transform:uppercase;margin-bottom:6px;margin-top:10px;}
.tax-year-filter{display:flex;gap:6px;padding:0 1rem;margin-bottom:.8rem;overflow-x:auto;scrollbar-width:none;}
.tax-year-filter::-webkit-scrollbar{display:none;}
.tax-year-tab{flex-shrink:0;padding:5px 12px;border-radius:16px;border:1px solid var(--cbm);background:var(--surface);color:var(--text2);font-size:12px;cursor:pointer;}
.tax-year-tab.active{background:var(--br);color:var(--cream);border-color:var(--br);}

/* ===== AI 分析タブ ===== */
.ai-header{background:linear-gradient(135deg,var(--dark) 0%,#5c3a1e 100%);color:var(--cream);padding:1.2rem 1.25rem 1rem;margin-bottom:1rem;}
.ai-header-title{font-size:16px;font-weight:700;display:flex;align-items:center;gap:8px;}
.ai-header-sub{font-size:11px;opacity:.65;margin-top:4px;}
.ai-week-selector{display:flex;overflow-x:auto;gap:6px;padding:0 1rem;margin-bottom:1rem;scrollbar-width:none;}
.ai-week-selector::-webkit-scrollbar{display:none;}
.ai-week-tab{flex-shrink:0;padding:6px 14px;border-radius:20px;border:1px solid var(--cbm);background:var(--surface);color:var(--text2);font-size:12px;cursor:pointer;white-space:nowrap;}
.ai-week-tab.active{background:var(--br);color:var(--cream);border-color:var(--br);}
.ai-stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;padding:0 1rem;margin-bottom:1rem;}
.ai-stat-card{background:var(--surface);border:.5px solid var(--cb);border-radius:12px;padding:12px 14px;}
.ai-stat-lbl{font-size:10px;color:var(--text3);font-weight:600;letter-spacing:.06em;text-transform:uppercase;}
.ai-stat-val{font-size:20px;font-weight:700;color:var(--br);margin-top:4px;}
.ai-stat-sub{font-size:10px;color:var(--text3);margin-top:2px;}
.ai-chart-wrap{padding:0 1rem;margin-bottom:1rem;}
.ai-chart-card{background:var(--surface);border:.5px solid var(--cb);border-radius:12px;padding:14px;overflow:hidden;}
.ai-chart-title{font-size:11px;font-weight:700;color:var(--text2);margin-bottom:10px;letter-spacing:.04em;}
.bar-chart{display:flex;align-items:flex-end;gap:6px;height:100px;}
.bar-item{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;}
.bar-fill{width:100%;border-radius:4px 4px 0 0;background:var(--br);min-height:2px;transition:height .3s;}
.bar-lbl{font-size:9px;color:var(--text3);}
.bar-val{font-size:8px;color:var(--text3);}
.ai-generate-btn{width:calc(100% - 2rem);margin:0 1rem 1rem;padding:14px;background:var(--dark);color:var(--cream);border:none;border-radius:12px;font-size:15px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;letter-spacing:.02em;}
.ai-generate-btn:active{opacity:.85;}
.ai-generate-btn:disabled{opacity:.5;cursor:default;}
.ai-result-box{margin:0 1rem 1rem;background:var(--surface);border:.5px solid var(--cb);border-radius:12px;padding:16px;font-size:13px;color:var(--text);line-height:1.8;white-space:pre-wrap;}
.ai-result-box.loading{color:var(--text3);font-style:italic;text-align:center;padding:24px;}
.ai-result-section{margin-bottom:12px;}
.ai-result-h{font-size:12px;font-weight:700;color:var(--br);text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px;}

/* ビュー切替 */
.view{display:none;}
.view.active{display:block;}

/* タブバー */
.tab-bar{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:430px;display:flex;justify-content:space-around;background:var(--surface);border-top:.5px solid var(--cb);padding:6px 0 env(safe-area-inset-bottom, 6px);z-index:100;box-shadow:0 -1px 6px rgba(107,63,30,.07);}
.tabbtn{display:flex;flex-direction:column;align-items:center;gap:2px;background:none;border:none;cursor:pointer;color:var(--text3);font-size:9px;padding:4px 6px;}
.tabbtn.active{color:var(--br);}
.tabbtn svg{width:20px;height:20px;stroke:currentColor;stroke-width:1.7;fill:none;}

/* 送信モーダル */
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:200;align-items:flex-end;justify-content:center;}
.modal-bg.open{display:flex;}
.modal-box{background:var(--surface);border-radius:18px 18px 0 0;width:100%;max-width:430px;padding:1.2rem 1.2rem calc(env(safe-area-inset-bottom,0px)+1.2rem);max-height:80vh;display:flex;flex-direction:column;gap:.8rem;overflow:hidden;}
.modal-title{font-size:15px;font-weight:700;color:var(--text);}
.modal-sub{font-size:11px;color:var(--text3);margin-top:2px;}
.modal-ta{width:100%;border:.5px solid var(--cbm);border-radius:8px;padding:10px;font-size:12px;color:var(--text);background:var(--cream);resize:none;flex:1;min-height:150px;max-height:250px;line-height:1.7;font-family:inherit;}
.modal-btns{display:flex;gap:8px;flex-shrink:0;}
.modal-copy{flex:1;padding:10px;border:.5px solid var(--cbm);border-radius:8px;background:none;color:var(--text2);font-size:13px;cursor:pointer;}
.modal-copy:active{background:var(--cream);}
.modal-line{flex:1;padding:10px;background:#06C755;color:#fff;border:none;border-radius:8px;font-size:13px;font-weight:600;cursor:pointer;}
.modal-close{width:100%;padding:9px;border:none;background:none;color:var(--text3);font-size:12px;cursor:pointer;}

/* タスク完了確認モーダル */
.task-modal-box{background:var(--surface);border-radius:18px 18px 0 0;width:100%;max-width:430px;padding:1.5rem 1.2rem calc(env(safe-area-inset-bottom,0px)+1.2rem);display:flex;flex-direction:column;gap:1rem;}
.task-modal-icon{font-size:40px;text-align:center;}
.task-modal-title{font-size:17px;font-weight:700;color:var(--text);text-align:center;}
.task-modal-sub{font-size:13px;color:var(--text2);text-align:center;line-height:1.6;}
.task-modal-detail{background:var(--cream);border-radius:10px;padding:12px 14px;font-size:12px;color:var(--text2);line-height:1.8;}
.task-modal-btns{display:flex;gap:8px;}
.task-modal-cancel{flex:1;padding:12px;border:.5px solid var(--cbm);border-radius:10px;background:none;color:var(--text2);font-size:14px;cursor:pointer;}
.task-modal-send{flex:2;padding:12px;background:var(--green);color:#fff;border:none;border-radius:10px;font-size:14px;font-weight:700;cursor:pointer;}
.task-modal-send:active{opacity:.85;}

/* 削除確認モーダル */
.confirm-modal-box{background:var(--surface);border-radius:18px 18px 0 0;width:100%;max-width:430px;padding:1.5rem 1.2rem calc(env(safe-area-inset-bottom,0px)+1.2rem);display:flex;flex-direction:column;gap:1rem;}
.confirm-modal-title{font-size:17px;font-weight:700;color:var(--text);text-align:center;}
.confirm-modal-sub{font-size:13px;color:var(--text2);text-align:center;line-height:1.6;}
.confirm-modal-detail{background:var(--redBg);border-radius:10px;padding:12px 14px;font-size:12px;color:var(--red);line-height:1.8;}
.confirm-modal-btns{display:flex;gap:8px;}
.confirm-cancel{flex:1;padding:12px;border:.5px solid var(--cbm);border-radius:10px;background:none;color:var(--text2);font-size:14px;cursor:pointer;}
.confirm-del{flex:1;padding:12px;background:var(--red);color:#fff;border:none;border-radius:10px;font-size:14px;font-weight:700;cursor:pointer;}
.confirm-del:active{opacity:.85;}

/* GAS設定モーダル */
.gas-modal-box{background:var(--surface);border-radius:18px 18px 0 0;width:100%;max-width:430px;padding:1.2rem 1.2rem calc(env(safe-area-inset-bottom,0px)+1.2rem);display:flex;flex-direction:column;gap:.8rem;}
.gas-input{width:100%;padding:12px;font-size:13px;border:.5px solid var(--cbm);border-radius:10px;color:var(--text);font-family:inherit;outline:none;background:var(--cream);}
.gas-input:focus{border-color:var(--br);}
.gas-save-btn{width:100%;padding:13px;background:var(--br);color:var(--cream);border:none;border-radius:10px;font-size:14px;font-weight:700;cursor:pointer;}
.gas-save-btn:active{opacity:.85;}
.gas-note{font-size:11px;color:var(--text3);line-height:1.6;}

/* 同期ステータス・GASセットアップガイド */
.sync-status-box{display:flex;align-items:center;gap:8px;padding:10px 12px;border-radius:9px;font-size:12px;font-weight:600;margin-top:4px;}
.sync-status-box.on{background:var(--greenBg);color:var(--green);}
.sync-status-box.off{background:#F0EBE3;color:var(--text2);}
.sync-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.sync-dot.on{background:var(--green);box-shadow:0 0 0 0 rgba(59,109,17,.6);animation:syncPulse 1.6s infinite;}
.sync-dot.off{background:var(--text3);}
@keyframes syncPulse{0%{box-shadow:0 0 0 0 rgba(59,109,17,.45);}70%{box-shadow:0 0 0 6px rgba(59,109,17,0);}100%{box-shadow:0 0 0 0 rgba(59,109,17,0);}}
.gas-setup-toggle{font-size:12px;color:var(--br);font-weight:600;cursor:pointer;padding:10px 0 4px;text-align:center;border-top:.5px solid var(--cbm);margin-top:8px;}
.gas-setup-guide{display:none;}
.gas-setup-guide.open{display:block;}
.gas-setup-step{font-size:12px;color:var(--text2);line-height:1.6;margin-bottom:8px;padding-left:26px;position:relative;}
.gas-step-num{position:absolute;left:0;top:0;width:18px;height:18px;border-radius:50%;background:var(--br);color:#fff;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;}
.gas-code-ta{width:100%;min-height:140px;max-height:200px;font-size:10px;font-family:monospace;border:.5px solid var(--cbm);border-radius:8px;padding:8px;background:var(--cream);color:var(--text);resize:none;line-height:1.5;margin:6px 0 10px;}
.pos-sync-indicator{display:inline-block;width:9px;height:9px;border-radius:50%;background:rgba(255,255,255,.35);vertical-align:middle;margin-left:4px;}
.pos-sync-indicator.on{background:#7FE0A0;box-shadow:0 0 0 0 rgba(127,224,160,.6);animation:syncPulse2 1.6s infinite;}
.pos-sync-indicator.off{background:rgba(255,255,255,.35);}
@keyframes syncPulse2{0%{box-shadow:0 0 0 0 rgba(127,224,160,.5);}70%{box-shadow:0 0 0 5px rgba(127,224,160,0);}100%{box-shadow:0 0 0 0 rgba(127,224,160,0);}}

/* データ保存場所バッジ */
.storage-info-box{margin:0 1rem 1rem;background:var(--blueBg);border:.5px solid #85B7EB;border-radius:12px;padding:12px 14px;}
.storage-info-box h4{font-size:12px;font-weight:700;color:var(--blue);margin-bottom:6px;}
.storage-info-box ul{list-style:none;padding:0;}
.storage-info-box li{font-size:11px;color:#185FA5;margin-bottom:4px;padding-left:12px;position:relative;line-height:1.5;}
.storage-info-box li::before{content:'›';position:absolute;left:0;color:var(--blue);}

/* ===== 営業終了サマリー ===== */
.dayclose-warn{background:var(--redBg);border:.5px solid #E0A8A0;border-radius:10px;padding:12px 14px;margin-bottom:1rem;font-size:12px;color:var(--red);line-height:1.7;}
.dayclose-stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:1rem;}
.dayclose-stat{background:var(--cream);border-radius:10px;padding:10px 12px;}
.dayclose-stat-lbl{font-size:10px;color:var(--text3);font-weight:600;}
.dayclose-stat-val{font-size:17px;font-weight:700;color:var(--br);margin-top:2px;}
.dayclose-section-hd{font-size:11px;font-weight:700;color:var(--text2);letter-spacing:.04em;margin:14px 0 6px;}
.dayclose-bar-row{display:flex;align-items:center;gap:8px;margin-bottom:6px;}
.dayclose-bar-lbl{font-size:11px;color:var(--text2);width:64px;flex-shrink:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.dayclose-bar-track{flex:1;background:var(--cb);border-radius:5px;height:14px;overflow:hidden;}
.dayclose-bar-fill{height:14px;background:var(--br);border-radius:5px;}
.dayclose-bar-val{font-size:11px;color:var(--text2);width:60px;text-align:right;flex-shrink:0;}
.dayclose-ta{width:100%;border:.5px solid var(--cbm);border-radius:8px;padding:10px;font-size:12px;color:var(--text);background:var(--cream);resize:none;min-height:180px;max-height:260px;line-height:1.7;font-family:inherit;margin-bottom:10px;}
.dayclose-history-row{display:flex;justify-content:space-between;align-items:center;padding:10px 12px;border-bottom:.5px solid var(--cb);font-size:12px;}
.dayclose-history-row:last-child{border-bottom:none;}
.dayclose-history-date{color:var(--text2);}
.dayclose-history-amt{font-weight:700;color:var(--br);}
.dayclose-history-row.clickable{cursor:pointer;}
.dayclose-history-row.clickable:active{background:var(--cream);}

/* タスク完了履歴 */
.task-hist-row{padding:11px 14px;border-bottom:.5px solid var(--cb);}
.task-hist-row:last-child{border-bottom:none;}
.task-hist-top{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:4px;}
.task-hist-date{font-size:12px;color:var(--text2);font-weight:600;}
.task-hist-progress{font-size:13px;font-weight:700;color:var(--br);}
.task-hist-staff{font-size:11px;color:var(--text3);}
.task-hist-detail{font-size:11px;color:var(--text3);line-height:1.7;white-space:pre-wrap;margin-top:4px;display:none;padding-top:4px;border-top:.5px dashed var(--cb);}
.task-hist-detail.open{display:block;}
.task-hist-tag{font-size:9px;padding:1px 6px;border-radius:6px;font-weight:700;margin-left:6px;}
.task-hist-tag.report{background:var(--greenBg);color:var(--green);}
.task-hist-tag.archive{background:#F0EBE3;color:var(--text2);}

/* ===== POSレジ ===== */
.pos-table-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;padding:0 1rem;margin-bottom:1rem;}
.pos-table-btn{position:relative;padding:14px 6px;border-radius:12px;border:1.5px solid var(--cbm);background:var(--surface);color:var(--text2);font-size:15px;font-weight:700;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:3px;}
.pos-table-btn.active{background:var(--br);color:var(--cream);border-color:var(--br);}
.pos-table-btn.has-order{border-color:var(--green);}
.pos-table-btn.has-order:not(.active){background:var(--greenBg);color:var(--green);}
.pos-table-sub{font-size:10px;opacity:.75;font-weight:500;}
.pos-table-badge{position:absolute;top:-6px;right:-6px;background:var(--red);color:#fff;font-size:10px;font-weight:700;border-radius:10px;min-width:18px;height:18px;display:flex;align-items:center;justify-content:center;padding:0 4px;}

.pos-current-bar{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;margin:0 1rem 1rem;background:var(--dark);border-radius:12px;color:var(--cream);}
.pos-current-tbl{font-size:15px;font-weight:700;}
.pos-current-sub{font-size:11px;opacity:.65;margin-top:2px;}
.pos-current-total{font-size:18px;font-weight:700;}

.pos-menu-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:8px;padding:0 14px 14px;}
.pos-menu-btn{position:relative;background:var(--cream);border:1.5px solid var(--cbm);border-radius:12px;padding:10px 8px;cursor:pointer;display:flex;flex-direction:column;align-items:flex-start;gap:2px;min-height:64px;text-align:left;}
.pos-menu-btn:active{background:var(--bl);border-color:var(--br);}
.pos-menu-btn.in-cart{border-color:var(--br);background:#FFF3E0;}
.pos-menu-name{font-size:12px;font-weight:600;color:var(--text);line-height:1.3;}
.pos-menu-price{font-size:11px;color:var(--text3);margin-top:auto;}
.pos-menu-cart-badge{position:absolute;top:-7px;right:-7px;background:var(--br);color:#fff;font-size:11px;font-weight:700;border-radius:50%;width:22px;height:22px;display:flex;align-items:center;justify-content:center;}

.pos-cart-card{margin:0 1rem 1rem;background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;}
.pos-cart-empty{padding:24px;text-align:center;color:var(--text3);font-size:13px;}
.pos-cart-row{display:flex;align-items:center;gap:10px;padding:10px 14px;border-bottom:.5px solid var(--cb);}
.pos-cart-row:last-child{border-bottom:none;}
.pos-cart-name{flex:1;font-size:13px;color:var(--text);}
.pos-cart-price{font-size:11px;color:var(--text3);}
.pos-cart-qty-ctrl{display:flex;align-items:center;gap:6px;}
.pos-cart-qbtn{width:26px;height:26px;border-radius:7px;border:1px solid var(--cbm);background:var(--surface);color:var(--br);font-size:16px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;line-height:1;}
.pos-cart-qbtn:active{background:var(--cream);}
.pos-cart-qval{font-size:14px;font-weight:700;color:var(--br);min-width:18px;text-align:center;}
.pos-cart-subtotal{font-size:13px;font-weight:700;color:var(--br);min-width:56px;text-align:right;}

.pos-confirm-btn{width:calc(100% - 2rem);margin:0 1rem 1rem;padding:13px;background:var(--green);color:#fff;border:none;border-radius:12px;font-size:14px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px;}
.pos-confirm-btn:active{opacity:.85;}
.pos-confirm-btn:disabled{opacity:.4;cursor:default;}

/* キッチン注文履歴（テーブルグループ化＋品目別チェック） */
.kitchen-group{margin:0 1rem 1rem;}
.kitchen-group-hd{display:flex;align-items:center;gap:8px;margin-bottom:6px;padding:0 2px;}
.kitchen-group-status{font-size:11px;color:var(--text2);font-weight:600;}
.kitchen-group.all-served .kitchen-group-status{color:var(--green);}
.kitchen-card{background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;}
.kitchen-tbl-badge{flex-shrink:0;padding:5px 12px;border-radius:9px;background:var(--br);color:var(--cream);font-size:14px;font-weight:700;}
.kitchen-order-block{border-bottom:1px solid var(--cb);}
.kitchen-order-block:last-child{border-bottom:none;}
.kitchen-order-time{font-size:10px;color:var(--text3);padding:8px 14px 0;}
.kitchen-item-row{display:flex;align-items:center;gap:10px;padding:9px 14px;cursor:pointer;transition:background .1s;}
.kitchen-item-row:active{background:var(--cream);}
.kitchen-item-row.served{opacity:.4;}
.kitchen-item-chk{width:22px;height:22px;border-radius:50%;border:1.5px solid var(--cbm);display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all .15s;}
.kitchen-item-row.served .kitchen-item-chk{background:var(--green);border-color:var(--green);}
.kitchen-item-name{flex:1;font-size:15px;font-weight:600;color:var(--text);line-height:1.3;}
.kitchen-item-row.served .kitchen-item-name{text-decoration:line-through;color:var(--text3);font-weight:400;}
.kitchen-item-qty{font-size:14px;font-weight:700;color:var(--br);flex-shrink:0;}
.kitchen-item-row.served .kitchen-item-qty{color:var(--text3);}

/* 会計分割（チェックボックス選択） */
.pos-checkout-card{margin:0 1rem 1rem;background:var(--surface);border:.5px solid var(--cb);border-radius:12px;overflow:hidden;}
.pos-checkout-row{display:flex;align-items:center;gap:10px;padding:10px 14px;border-bottom:.5px solid var(--cb);}
.pos-checkout-row:last-child{border-bottom:none;}
.pos-checkout-chk{width:21px;height:21px;border-radius:6px;border:1.5px solid var(--cbm);display:flex;align-items:center;justify-content:center;flex-shrink:0;cursor:pointer;}
.pos-checkout-chk.checked{background:var(--br);border-color:var(--br);}
.pos-checkout-name{flex:1;font-size:13px;color:var(--text);}
.pos-checkout-amt{font-size:13px;font-weight:700;color:var(--br);}
.pos-split-toolbar{display:flex;gap:8px;padding:0 1rem;margin-bottom:.8rem;}
.pos-split-btn{flex:1;padding:8px;border-radius:9px;border:1px solid var(--cbm);background:var(--surface);color:var(--text2);font-size:12px;font-weight:600;cursor:pointer;}
.pos-split-btn:active{background:var(--cream);}

/* お預かり・おつり */
.cash-row{display:flex;align-items:center;gap:10px;padding:10px 14px;}
.cash-input{flex:1;padding:9px 10px;font-size:16px;border:.5px solid var(--cbm);border-radius:8px;color:var(--text);background:var(--bg);font-family:inherit;outline:none;text-align:right;}
.cash-quick-row{display:flex;gap:6px;padding:0 14px 10px;flex-wrap:wrap;}
.cash-quick-btn{flex:1;min-width:60px;padding:8px 4px;text-align:center;font-size:12px;font-weight:600;border-radius:8px;border:1px solid var(--cbm);background:var(--surface);color:var(--text2);cursor:pointer;}
.cash-quick-btn:active{background:var(--cream);}
.change-display{display:flex;justify-content:space-between;align-items:center;padding:12px 14px;background:var(--cream);}
.change-lbl{font-size:13px;color:var(--text2);}
.change-val{font-size:22px;font-weight:700;color:var(--green);}
.change-val.negative{color:var(--red);}

/* ドリンク選択モーダル（セット用） */
.drink-select-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;padding:0 0 4px;}
.drink-select-btn{background:var(--cream);border:1.5px solid var(--cbm);border-radius:12px;padding:12px 10px;cursor:pointer;text-align:center;font-size:13px;font-weight:600;color:var(--text);}
.drink-select-btn:active{background:var(--bl);border-color:var(--br);color:#fff;}
.drink-select-set-name{font-size:13px;color:var(--text2);background:var(--cream);border-radius:8px;padding:8px 12px;margin-bottom:10px;}
</style>
</head>
<body>
<div class="app">

<!-- ヘッダー（タスクのみ） -->
<div class="header" id="task-header">
  <div class="hrow">
    <div>
      <div class="htitle">☕ 喫茶すず タスク帳</div>
      <div class="hdate" id="hdate"></div>
    </div>
    <div class="hright">
      <div class="hnum" id="prog-num">0/0</div>
      <div class="hlbl">本日完了</div>
    </div>
  </div>
  <div class="pbar-wrap"><div class="pbar-fill" id="pbar" style="width:0%"></div></div>
  <div class="pbar-row"><span>進捗</span><span id="prog-pct">0%</span></div>
</div>
<div class="dtabs" id="dtabs" style="display:none;"></div>

<!-- ===== タスクビュー ===== -->
<div class="view active" id="view-tasks"></div>

<!-- ===== 買い出しビュー ===== -->
<div class="view" id="view-buy"></div>

<!-- ===== POSレジ（会計入力）ビュー ===== -->
<div class="view" id="view-report">
  <div class="rep-header">
    <div class="rep-header-title">🧾 POSレジ <span class="pos-sync-indicator" id="pos-sync-indicator-report" title="未設定"></span></div>
    <div class="rep-header-sub">テーブルを選んでメニューをタップ→注文確定</div>
  </div>

  <div class="daily-info-banner" id="daily-info-banner">
    <div class="daily-info-header">
      <span class="daily-info-lbl">📌 本日の固定情報</span>
      <span class="daily-info-edit" onclick="toggleDailyEdit()">✏️ 変更</span>
    </div>
    <div class="daily-info-row" id="daily-info-display">
      <div class="daily-info-empty" id="daily-info-empty">担当者名・天気を設定してください</div>
      <div class="daily-info-chip" id="chip-staff" style="display:none;">
        <span>担当者</span><strong id="chip-staff-val">—</strong>
      </div>
      <div class="daily-info-chip" id="chip-weather" style="display:none;">
        <span>天気</span><strong id="chip-weather-val">—</strong>
      </div>
    </div>
    <div class="daily-info-edit-area" id="daily-edit-area">
      <label class="field-lbl">担当者名</label>
      <input type="text" id="daily-staff-input" placeholder="例：山田">
      <label class="field-lbl" style="margin-top:10px;">天気</label>
      <div class="weather-radio" id="daily-weather-radio">
        <div class="weather-radio-btn" onclick="setDailyWeather('晴れ')">☀️ 晴れ</div>
        <div class="weather-radio-btn" onclick="setDailyWeather('曇り')">☁️ 曇り</div>
        <div class="weather-radio-btn" onclick="setDailyWeather('雨')">🌧 雨</div>
      </div>
      <button class="daily-save-btn" onclick="saveDailyInfo()">設定を保存する</button>
    </div>
  </div>

  <div style="padding:0 1rem;margin-bottom:1rem;">
    <button class="reset-btn" style="margin:0;width:100%;background:var(--dark);color:var(--cream);border:none;font-size:13px;font-weight:700;padding:11px;" onclick="openDayCloseModal()">
      🌙 本日の営業を終了する（売上サマリー）
    </button>
  </div>
  <div style="padding:0 1rem;margin-bottom:1rem;">
    <button class="reset-btn" style="margin:0;width:100%;" onclick="openGasModal()">
      🔄 リアルタイム同期設定（複数端末で共有）
    </button>
  </div>

  <div class="sec-lbl" style="padding:0 1rem;margin-bottom:.4rem;">テーブルを選択</div>
  <div class="pos-table-grid" id="pos-table-grid"></div>

  <div id="pos-current-bar-area"></div>

  <div id="pos-main-area"></div>

</div>

<!-- ===== キッチン注文履歴ビュー ===== -->
<div class="view" id="view-kitchen">
  <div class="rep-header">
    <div class="rep-header-title">🍳 キッチン注文履歴 <span class="pos-sync-indicator" id="pos-sync-indicator-kitchen" title="未設定"></span></div>
    <div class="rep-header-sub">注文確定された順に表示されます</div>
  </div>
  <div style="padding:0 1rem;margin-bottom:.8rem;display:flex;gap:8px;">
    <button class="reset-btn" style="margin:0;flex:1;" onclick="clearServedKitchen()">提供済みを一覧から消す</button>
  </div>
  <div id="kitchen-list-area"></div>
</div>


<!-- ===== 会計履歴ビュー ===== -->
<div class="view" id="view-history">
  <div class="rep-header">
    <div class="rep-header-title">📈 会計履歴</div>
    <div class="rep-header-sub">明細行の ✕ ボタンで個別取り消しができます</div>
  </div>
  <div id="hist-date-filter" class="date-filter"></div>
  <div id="hist-day-total" class="day-total-bar" style="display:none;">
    <div><div class="day-total-lbl">選択日の合計売上</div><div class="day-count" id="hist-day-count"></div></div>
    <div class="day-total-val" id="hist-day-total-val"></div>
  </div>
  <div id="hist-content"></div>
</div>

<!-- ===== 経費・支出ビュー ===== -->
<div class="view" id="view-expense">
  <div class="rep-header">
    <div class="rep-header-title">💰 経費・支出管理</div>
    <div class="rep-header-sub">仕入・光熱費・消耗品などを記録します</div>
  </div>

  <!-- 経費入力フォーム -->
  <div class="form-row">
    <div class="form-lbl">支出日</div>
    <div class="form-card">
      <div class="field-wrap">
        <input class="field-input" type="date" id="exp-date">
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="form-lbl">カテゴリ</div>
    <div class="form-card">
      <div class="radio-group" id="exp-cat-group">
        <div class="radio-btn" onclick="setExpCat('食材・仕入')">食材・仕入</div>
        <div class="radio-btn" onclick="setExpCat('光熱費')">光熱費</div>
        <div class="radio-btn" onclick="setExpCat('消耗品')">消耗品</div>
        <div class="radio-btn" onclick="setExpCat('その他')">その他</div>
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="form-lbl">内容・摘要</div>
    <div class="form-card">
      <div class="field-wrap">
        <input class="field-input" type="text" id="exp-name" placeholder="例：業務スーパー　食材仕入れ">
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="form-lbl">金額（税込）</div>
    <div class="form-card">
      <div class="field-wrap">
        <input class="field-input" type="number" id="exp-amount" placeholder="例：5800" min="0">
      </div>
    </div>
  </div>
  <div class="form-row">
    <div class="form-lbl">領収書番号（任意）</div>
    <div class="form-card">
      <div class="field-wrap">
        <input class="field-input" type="text" id="exp-receipt-no" placeholder="例：R-20240601-001">
      </div>
    </div>
  </div>
  <div class="msg-box" id="exp-msg"></div>
  <button class="submit-btn" onclick="submitExpense()">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>
    経費を登録する
  </button>

  <!-- 経費一覧 -->
  <div style="padding:0 1rem;margin-bottom:.5rem;margin-top:.5rem;">
    <div class="form-lbl">登録済み経費</div>
  </div>
  <div class="tax-year-filter" id="exp-year-filter"></div>
  <div id="exp-list-area"></div>

  <!-- 確定申告サマリ -->
  <div style="padding:0 1rem;margin-bottom:.5rem;margin-top:.5rem;">
    <div class="form-lbl">確定申告 年次サマリ</div>
  </div>
  <div id="exp-year-select-row" style="padding:0 1rem;margin-bottom:.8rem;display:flex;gap:8px;flex-wrap:wrap;"></div>
  <div id="tax-summary-area"></div>

  <div class="storage-info-box">
    <h4>💾 データ保存場所について</h4>
    <ul>
      <li><strong>会計データ</strong>：このブラウザの localStorage（キー: suzu_receipts_v2）</li>
      <li><strong>経費データ</strong>：このブラウザの localStorage（キー: suzu_expenses_v1）</li>
      <li><strong>タスク記録</strong>：このブラウザの localStorage（キー: suzu_task_done_v4, suzu_tasklog_v1）</li>
      <li><strong>買い出し</strong>：このブラウザの localStorage（キー: suzu_buy_done_v4）</li>
      <li><strong>営業終了サマリー</strong>：このブラウザの localStorage（キー: suzu_dayclose_v1）</li>
      <li><strong>GAS連携時</strong>：Googleスプレッドシートにも同時保存</li>
      <li>※ ブラウザのキャッシュ削除・プライベートモード・別端末では参照不可</li>
    </ul>
  </div>
</div>

<!-- ===== AI 売上分析ビュー ===== -->
<div class="view" id="view-ai">
  <div class="ai-header">
    <div class="ai-header-title">🤖 週次売上分析</div>
    <div class="ai-header-sub">週単位で売上を集計し、AIが改善策を提案します</div>
  </div>

  <div class="ai-week-selector" id="ai-week-selector"></div>
  <div class="ai-stats-grid" id="ai-stats-grid"></div>

  <div class="ai-chart-wrap">
    <div class="ai-chart-card">
      <div class="ai-chart-title">売上内訳（カテゴリ別）</div>
      <div id="ai-menu-chart"></div>
    </div>
  </div>

  <div class="ai-chart-wrap">
    <div class="ai-chart-card">
      <div class="ai-chart-title">時間帯別 組数</div>
      <div id="ai-hour-chart"></div>
    </div>
  </div>

  <div class="ai-chart-wrap">
    <div class="ai-chart-card">
      <div class="ai-chart-title">客層別 売上</div>
      <div id="ai-customer-chart"></div>
    </div>
  </div>

  <button class="ai-generate-btn" id="ai-gen-btn" onclick="generateAIAnalysis()">
    ✨ AI で売上向上策を提案する
  </button>
  <div id="ai-result-area"></div>
</div>

<!-- タブバー -->
<div class="tab-bar">
  <button class="tabbtn active" id="tab-tasks" onclick="switchTab('tasks',this)">
    <svg viewBox="0 0 24 24"><path d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2"/><rect x="9" y="3" width="6" height="4" rx="1"/><path d="M9 12l2 2 4-4"/></svg>
    タスク
  </button>
  <button class="tabbtn" id="tab-buy" onclick="switchTab('buy',this)">
    <svg viewBox="0 0 24 24"><path d="M6 2L3 6v14a2 2 0 002 2h14a2 2 0 002-2V6l-3-4z"/><line x1="3" y1="6" x2="21" y2="6"/><path d="M16 10a4 4 0 01-8 0"/></svg>
    買い出し
  </button>
  <button class="tabbtn" id="tab-report" onclick="switchTab('report',this)">
    <svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="9" y1="21" x2="9" y2="3"/></svg>
    レジ
  </button>
  <button class="tabbtn" id="tab-kitchen" onclick="switchTab('kitchen',this)">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><path d="M12 7v5l3 3"/></svg>
    キッチン
  </button>
  <button class="tabbtn" id="tab-history" onclick="switchTab('history',this)">
    <svg viewBox="0 0 24 24"><path d="M12 20V10"/><path d="M18 20V4"/><path d="M6 20v-4"/></svg>
    履歴
  </button>
  <button class="tabbtn" id="tab-expense" onclick="switchTab('expense',this)">
    <svg viewBox="0 0 24 24"><path d="M12 2a10 10 0 100 20A10 10 0 0012 2z"/><path d="M12 6v6l4 2"/></svg>
    経費
  </button>
  <button class="tabbtn" id="tab-ai" onclick="switchTab('ai',this)">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M20.2 7.8l-1.4-1.4-2.1 2.1M3.8 7.8l1.4-1.4 2.1 2.1M12 3V1M12 23v-2M4.2 16.2l-1.4 1.4 2.1-2.1M19.8 16.2l1.4 1.4-2.1-2.1"/></svg>
    AI分析
  </button>
</div>

</div><!-- /app -->

<!-- 買い出し送信モーダル -->
<div class="modal-bg" id="send-modal-bg" onclick="closeSendModal(event)">
  <div class="modal-box">
    <div>
      <div class="modal-title">📋 買い出しリストを送信</div>
      <div class="modal-sub" id="modal-sub"></div>
    </div>
    <div id="modal-content" style="display:flex;flex-direction:column;flex:1;overflow:hidden;"></div>
    <div class="modal-btns" id="modal-btns">
      <button class="modal-copy" onclick="copyList()">📋 コピー</button>
      <button class="modal-line" onclick="openLine()">LINE で送る</button>
    </div>
    <button class="modal-close" onclick="closeSendModal()">閉じる</button>
  </div>
</div>

<!-- タスク完了確認モーダル -->
<div class="modal-bg" id="task-modal-bg">
  <div class="task-modal-box">
    <div class="task-modal-icon">✅</div>
    <div class="task-modal-title">本日のタスクを完了報告</div>
    <div class="task-modal-sub">完了状況をシートに記録します。<br>担当者名を入力してください。</div>
    <div class="form-card">
      <div class="field-wrap">
        <span class="field-lbl">担当者名</span>
        <input class="field-input" type="text" id="task-staff-input" placeholder="例：山田">
      </div>
    </div>
    <div class="task-modal-detail" id="task-modal-detail"></div>
    <div class="task-modal-btns">
      <button class="task-modal-cancel" onclick="closeTaskModal()">キャンセル</button>
      <button class="task-modal-send" onclick="sendTaskReport()">シートに記録する</button>
    </div>
    <div class="msg-box" id="task-modal-msg" style="margin:0;"></div>
  </div>
</div>

<!-- 削除確認モーダル -->
<div class="modal-bg" id="confirm-modal-bg">
  <div class="confirm-modal-box">
    <div class="confirm-modal-title">⚠️ この会計を取り消しますか？</div>
    <div class="confirm-modal-sub">一度削除すると元に戻せません。</div>
    <div class="confirm-modal-detail" id="confirm-modal-detail"></div>
    <div class="confirm-modal-btns">
      <button class="confirm-cancel" onclick="closeConfirmModal()">キャンセル</button>
      <button class="confirm-del" onclick="executeDelete()">取り消す</button>
    </div>
  </div>
</div>

<!-- ドリンク選択モーダル（セット用） -->
<div class="modal-bg" id="drink-select-modal-bg">
  <div class="modal-box" style="max-height:75vh;">
    <div>
      <div class="modal-title">🥤 ドリンクを選択</div>
      <div class="modal-sub" id="drink-select-sub"></div>
    </div>
    <div id="drink-select-content" style="overflow-y:auto;flex:1;"></div>
    <button class="modal-close" onclick="closeDrinkSelectModal()">キャンセル</button>
  </div>
</div>

<!-- 会計（チェックアウト）モーダル -->
<div class="modal-bg" id="checkout-modal-bg">
  <div class="modal-box" style="max-height:88vh;">
    <div>
      <div class="modal-title">💴 お会計</div>
      <div class="modal-sub" id="checkout-modal-sub"></div>
    </div>
    <div id="checkout-modal-content" style="overflow-y:auto;flex:1;"></div>
    <button class="modal-close" onclick="closeCheckoutModal()">閉じる</button>
  </div>
</div>

<!-- 営業終了・本日の売上サマリーモーダル -->
<div class="modal-bg" id="dayclose-modal-bg">
  <div class="modal-box" style="max-height:88vh;">
    <div>
      <div class="modal-title">🌙 本日の営業終了</div>
      <div class="modal-sub" id="dayclose-modal-sub"></div>
    </div>
    <div id="dayclose-modal-content" style="overflow-y:auto;flex:1;"></div>
    <button class="modal-close" onclick="closeDayCloseModal()">閉じる</button>
  </div>
</div>

<!-- タスク完了履歴モーダル -->
<div class="modal-bg" id="task-history-modal-bg">
  <div class="modal-box" style="max-height:85vh;">
    <div>
      <div class="modal-title">📜 タスク完了履歴</div>
      <div class="modal-sub">過去に報告・記録されたタスク完了状況（削除されません）</div>
    </div>
    <div id="task-history-content" style="overflow-y:auto;flex:1;"></div>
    <button class="modal-close" onclick="closeTaskHistoryModal()">閉じる</button>
  </div>
</div>

<!-- GAS設定モーダル -->
<div class="modal-bg" id="gas-modal-bg" onclick="closeGasModal(event)">
  <div class="gas-modal-box" style="max-height:85vh;overflow-y:auto;">
    <div class="modal-title">⚙️ GAS連携・リアルタイム同期設定</div>
    <p class="gas-note">Google Apps Script のウェブアプリURLを設定すると、①会計・経費がスプレッドシートに自動保存され、②複数の端末間でPOSのカート・キッチン注文がリアルタイムに共有されます。</p>
    <input class="gas-input" type="url" id="gas-url-input" placeholder="https://script.google.com/macros/s/...">
    <button class="gas-save-btn" onclick="saveGasUrl()">保存する</button>

    <div class="sync-status-box" id="sync-status-box"></div>

    <div class="gas-setup-toggle" onclick="toggleGasSetupGuide()">📖 セットアップ手順を見る（初回のみ）</div>
    <div class="gas-setup-guide" id="gas-setup-guide">
      <div class="gas-setup-step"><span class="gas-step-num">1</span>新しい Google スプレッドシートを開く</div>
      <div class="gas-setup-step"><span class="gas-step-num">2</span>「拡張機能」→「Apps Script」を開く</div>
      <div class="gas-setup-step"><span class="gas-step-num">3</span>下のコードを全部コピーして貼り付け（既存コードは削除）</div>
      <textarea class="gas-code-ta" id="gas-code-ta" readonly></textarea>
      <button class="modal-copy" style="width:100%;margin-bottom:10px;" onclick="copyGasCode()">📋 コードをコピー</button>
      <div class="gas-setup-step"><span class="gas-step-num">4</span>「デプロイ」→「新しいデプロイ」→ 種類「ウェブアプリ」を選択</div>
      <div class="gas-setup-step"><span class="gas-step-num">5</span>アクセスできるユーザー：「全員」に設定して「デプロイ」</div>
      <div class="gas-setup-step"><span class="gas-step-num">6</span>表示されたURLをコピーし、上の入力欄に貼って保存</div>
      <div class="gas-setup-step"><span class="gas-step-num">7</span>他のスタッフの端末でも同じURLを設定すれば同期されます</div>
    </div>

    <button class="modal-close" onclick="closeGasModal()">閉じる</button>
  </div>
</div>

<script>
/* ============================================================
   GAS URL ・ リアルタイム同期
   ============================================================ */
const GAS_URL_KEY = 'suzu_gas_url';
function getGasUrl(){ return localStorage.getItem(GAS_URL_KEY)||''; }
function saveGasUrl(){
  const v = document.getElementById('gas-url-input').value.trim();
  if(v) localStorage.setItem(GAS_URL_KEY,v);
  else localStorage.removeItem(GAS_URL_KEY);
  renderSyncStatusBox();
  startSyncPolling();
  syncPullNow();
}
function openGasModal(){
  document.getElementById('gas-url-input').value = getGasUrl();
  document.getElementById('gas-code-ta').value = GAS_CODE_TEMPLATE;
  renderSyncStatusBox();
  document.getElementById('gas-modal-bg').classList.add('open');
}
function closeGasModal(e){
  if(e && e.target !== document.getElementById('gas-modal-bg')) return;
  document.getElementById('gas-modal-bg').classList.remove('open');
}
function toggleGasSetupGuide(){
  document.getElementById('gas-setup-guide').classList.toggle('open');
}
async function copyGasCode(){
  try{ await navigator.clipboard.writeText(GAS_CODE_TEMPLATE); const btn=document.querySelector('#gas-modal-bg .modal-copy'); if(btn){btn.textContent='✅ コピーしました'; setTimeout(()=>btn.textContent='📋 コードをコピー',2000);} }
  catch{ const ta=document.getElementById('gas-code-ta'); ta.select(); document.execCommand('copy'); }
}
function renderSyncStatusBox(){
  const box=document.getElementById('sync-status-box');
  if(!box)return;
  const url=getGasUrl();
  if(url){
    box.className='sync-status-box on';
    box.innerHTML='<span class="sync-dot on"></span>リアルタイム同期：有効（15秒ごとに自動更新）';
  }else{
    box.className='sync-status-box off';
    box.innerHTML='<span class="sync-dot off"></span>リアルタイム同期：未設定（端末内のみで動作）';
  }
}

/* GASに貼り付けるサーバーコード（コピー用テンプレート文字列） */
const GAS_CODE_TEMPLATE = `function doPost(e) {
  var data = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();

  // ---- リアルタイム同期用（カート・キッチン） ----
  if (data.type === 'sync_push') {
    var syncSheet = ss.getSheetByName('Sync') || ss.insertSheet('Sync');
    syncSheet.getRange('A1').setValue('posCarts');
    syncSheet.getRange('B1').setValue(JSON.stringify(data.posCarts || {}));
    syncSheet.getRange('A2').setValue('kitchen');
    syncSheet.getRange('B2').setValue(JSON.stringify(data.kitchen || []));
    syncSheet.getRange('A3').setValue('updatedAt');
    syncSheet.getRange('B3').setValue(new Date().toISOString());
    return ContentService.createTextOutput(JSON.stringify({status:'ok'})).setMimeType(ContentService.MimeType.JSON);
  }

  // ---- 会計データ ----
  if (data.type === 'receipt') {
    var sheet = ss.getSheetByName('会計') || ss.insertSheet('会計');
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(['日付','曜日','時刻','担当','卓','人数','客層','天気','注文','小計','税','合計','客単価','メモ','保存時刻']);
    }
    sheet.appendRow([data.date,data.youbi,data.time,data.staff,data.table,data.people,data.customer,data.weather,data.order,data.subtotal,data.tax,data.grand,data.unitPrice,data.memo,data.savedAt]);
    return ContentService.createTextOutput(JSON.stringify({status:'ok'})).setMimeType(ContentService.MimeType.JSON);
  }

  // ---- 経費データ ----
  if (data.type === 'expense') {
    var expSheet = ss.getSheetByName('経費') || ss.insertSheet('経費');
    if (expSheet.getLastRow() === 0) {
      expSheet.appendRow(['日付','カテゴリ','内容','金額','領収書番号','保存時刻']);
    }
    expSheet.appendRow([data.date,data.cat,data.name,data.amount,data.receiptNo,data.savedAt]);
    return ContentService.createTextOutput(JSON.stringify({status:'ok'})).setMimeType(ContentService.MimeType.JSON);
  }

  // ---- タスク完了報告 ----
  if (data.type === 'task') {
    var taskSheet = ss.getSheetByName('タスク') || ss.insertSheet('タスク');
    if (taskSheet.getLastRow() === 0) {
      taskSheet.appendRow(['日付','曜日','時刻','担当','曜日区分','完了数','合計数','詳細']);
    }
    taskSheet.appendRow([data.date,data.youbi,data.time,data.staff,data.taskDay,data.done,data.total,data.detail]);
    return ContentService.createTextOutput(JSON.stringify({status:'ok'})).setMimeType(ContentService.MimeType.JSON);
  }

  return ContentService.createTextOutput(JSON.stringify({status:'ok'})).setMimeType(ContentService.MimeType.JSON);
}

function doGet(e) {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  if (e.parameter.type === 'sync_pull') {
    var syncSheet = ss.getSheetByName('Sync');
    if (!syncSheet) {
      return ContentService.createTextOutput(JSON.stringify({posCarts:{},kitchen:[],updatedAt:null})).setMimeType(ContentService.MimeType.JSON);
    }
    var posCarts = JSON.parse(syncSheet.getRange('B1').getValue() || '{}');
    var kitchen = JSON.parse(syncSheet.getRange('B2').getValue() || '[]');
    var updatedAt = syncSheet.getRange('B3').getValue();
    return ContentService.createTextOutput(JSON.stringify({posCarts:posCarts,kitchen:kitchen,updatedAt:updatedAt})).setMimeType(ContentService.MimeType.JSON);
  }
  return ContentService.createTextOutput(JSON.stringify({status:'ok'})).setMimeType(ContentService.MimeType.JSON);
}`;

/* ---- 同期処理本体 ---- */
let syncPollTimer=null;
let lastSyncPushAt=0;
const SYNC_POLL_INTERVAL=15000; // 15秒ごと
let syncInFlight=false;

function startSyncPolling(){
  if(syncPollTimer) clearInterval(syncPollTimer);
  if(!getGasUrl()) return;
  syncPollTimer=setInterval(syncPullNow, SYNC_POLL_INTERVAL);
}

async function syncPullNow(){
  const url=getGasUrl();
  if(!url || syncInFlight) return;
  syncInFlight=true;
  try{
    const res=await fetch(url+(url.includes('?')?'&':'?')+'type=sync_pull');
    const json=await res.json();
    if(json && typeof json==='object'){
      if(json.posCarts) { posCarts=json.posCarts; lsSet(SK_POS_CARTS,posCarts); }
      if(json.kitchen) { lsSet(SK_KITCHEN,json.kitchen); }
      // 現在表示中のビューを更新
      const reportView=document.getElementById('view-report');
      if(reportView && reportView.classList.contains('active')){ renderPosTableGrid(); renderPosMain(); }
      const kitchenView=document.getElementById('view-kitchen');
      if(kitchenView && kitchenView.classList.contains('active')){ renderKitchenList(); }
      updateSyncIndicators(true);
    }
  }catch(e){
    updateSyncIndicators(false);
  }
  syncInFlight=false;
}

async function syncPushNow(){
  const url=getGasUrl();
  if(!url) return;
  lastSyncPushAt=Date.now();
  try{
    await fetch(url,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({
      type:'sync_push', posCarts:posCarts, kitchen:lsGet(SK_KITCHEN,[])
    })});
    updateSyncIndicators(true);
  }catch(e){
    updateSyncIndicators(false);
  }
}

function updateSyncIndicators(ok){
  document.querySelectorAll('.pos-sync-indicator').forEach(el=>{
    el.className='pos-sync-indicator'+(ok?' on':' off');
    el.title = ok ? '同期OK' : '同期エラー';
  });
}

/* ============================================================
   日次固定情報
   ============================================================ */
const SK_DAILY_INFO = 'suzu_daily_info_v1';
let dailyInfo = { staff:'', weather:'', date:'' };

function loadDailyInfo(){
  try{
    const raw = localStorage.getItem(SK_DAILY_INFO);
    if(!raw) return;
    const d = JSON.parse(raw);
    const today = todayDateStr();
    if(d.date !== today){
      dailyInfo = { staff: d.staff||'', weather:'', date: today };
      saveDailyInfoToStorage();
    } else {
      dailyInfo = d;
    }
  }catch(e){}
}
function todayDateStr(){
  const d = new Date();
  return d.getFullYear()+'-'+(d.getMonth()+1)+'-'+d.getDate();
}
function saveDailyInfoToStorage(){
  try{ localStorage.setItem(SK_DAILY_INFO, JSON.stringify(dailyInfo)); }catch(e){}
}
let dailyEditWeather = '';
function toggleDailyEdit(){
  const area = document.getElementById('daily-edit-area');
  area.classList.toggle('open');
  if(area.classList.contains('open')){
    document.getElementById('daily-staff-input').value = dailyInfo.staff;
    dailyEditWeather = dailyInfo.weather;
    updateWeatherRadio();
  }
}
function setDailyWeather(v){ dailyEditWeather = v; updateWeatherRadio(); }
function updateWeatherRadio(){
  document.querySelectorAll('#daily-weather-radio .weather-radio-btn').forEach(b=>{
    b.classList.toggle('active', b.textContent.includes(dailyEditWeather));
  });
}
function saveDailyInfo(){
  const staff = document.getElementById('daily-staff-input').value.trim();
  if(!staff){ alert('担当者名を入力してください'); return; }
  if(!dailyEditWeather){ alert('天気を選択してください'); return; }
  dailyInfo.staff = staff;
  dailyInfo.weather = dailyEditWeather;
  dailyInfo.date = todayDateStr();
  saveDailyInfoToStorage();
  document.getElementById('daily-edit-area').classList.remove('open');
  renderDailyInfoBanner();
}
function renderDailyInfoBanner(){
  const chipStaff = document.getElementById('chip-staff');
  const chipWeather = document.getElementById('chip-weather');
  const empty = document.getElementById('daily-info-empty');
  if(dailyInfo.staff || dailyInfo.weather){
    empty.style.display = 'none';
    if(dailyInfo.staff){ chipStaff.style.display = 'flex'; document.getElementById('chip-staff-val').textContent = dailyInfo.staff; }
    else chipStaff.style.display = 'none';
    if(dailyInfo.weather){
      chipWeather.style.display = 'flex';
      const wMap = {'晴れ':'☀️ 晴れ','曇り':'☁️ 曇り','雨':'🌧 雨'};
      document.getElementById('chip-weather-val').textContent = wMap[dailyInfo.weather]||dailyInfo.weather;
    } else chipWeather.style.display = 'none';
  } else {
    empty.style.display = 'block';
    chipStaff.style.display = 'none';
    chipWeather.style.display = 'none';
  }
}

/* ============================================================
   ストレージ
   ============================================================ */
const SK_TASK     = 'suzu_task_done_v4';
const SK_BUY      = 'suzu_buy_done_v4';
const SK_RECEIPT  = 'suzu_receipts_v2';
const SK_TASKLOG  = 'suzu_tasklog_v1';
const SK_EXPENSE  = 'suzu_expenses_v1';

let taskDone = {};
let buyState  = {};

function lsGet(k,def={}){ try{const v=localStorage.getItem(k);return v?JSON.parse(v):def;}catch{return def;} }
function lsSet(k,v){ try{localStorage.setItem(k,JSON.stringify(v));}catch{} }

/* ============================================================
   タスクデータ
   ============================================================ */
const DAYS=['月','火','水','木','金','土','日'];
const jsDay=new Date().getDay();
const todayIdx=jsDay===0?6:jsDay-1;
let selDay=DAYS[todayIdx];

const CLEAN={
  月:{name:'棚・収納棚の清掃',note:'全棚を乾拭き・整頓'},
  火:{name:'鏡・鏡面清掃',note:'入口・トイレ鏡をガラスクリーナーで'},
  水:{name:'床清掃（全フロア）',note:'モップがけ・隅まで丁寧に'},
  木:{name:'ガラス清掃',note:'窓・仕切りガラス全て'},
  金:{name:'トイレ清掃（念入り）',note:'便器・床・壁・手すりを全部'},
  土:{name:'グリストラップ清掃',note:'油脂除去・フィルター洗浄'},
  日:{name:'外部・外掃除',note:'店前・看板周り・駐輪場'},
};
const DAY_TASKS={
  月:[
    {id:'m1',name:'塩の固まり確認・補充',note:'テーブル塩入れ全て確認',type:'dy'},
    {id:'m2',name:'グリストラップ段ボールカット',note:'適切なサイズに切る',type:'dy'},
    {id:'m3',name:'砂糖スプーン清掃',note:'全スプーン水洗い・乾燥',type:'dy'},
    {id:'m4',name:'カップ・コップ・フォーク数報告',note:'不足数をノートに記入',type:'dy'},
  ],
  火:[
    {id:'k1',name:'ゴミ袋まとめ・縛る',note:'',type:'dy'},
    {id:'k2',name:'収集所へ持ち出し',note:'収集時間を事前確認',type:'dy'},
    {id:'k3',name:'ゴミ箱清掃・新袋セット',note:'',type:'dy'},
  ],
  水:[
    {id:'w1',name:'ユニフォーム・タオル投入',note:'洗剤量を確認',type:'dy'},
    {id:'w2',name:'洗濯機スタート',note:'標準コース',type:'dy'},
    {id:'w3',name:'乾燥・畳んで収納',note:'所定の場所へ',type:'dy'},
  ],
  木:[{id:'t1',name:'買い出しリスト確認',note:'買い出しタブでチェック',type:'op'}],
  金:[
    {id:'f1',name:'ゴミ袋まとめ・縛る',note:'',type:'dy'},
    {id:'f2',name:'収集所へ持ち出し',note:'収集時間を事前確認',type:'dy'},
    {id:'f3',name:'ゴミ箱清掃・新袋セット',note:'',type:'dy'},
  ],
  土:[
    {id:'sa1',name:'ユニフォーム・タオル投入',note:'',type:'dy'},
    {id:'sa2',name:'洗濯機スタート',note:'標準コース',type:'dy'},
    {id:'sa3',name:'乾燥・畳んで収納',note:'',type:'dy'},
  ],
  日:[{id:'su1',name:'買い出しリスト確認',note:'買い出しタブでチェック',type:'op'}],
};
const DAILY=[
  {id:'d1',name:'開店準備（看板・照明・BGM）',note:'',type:'op'},
  {id:'d2',name:'POSレジ起動・釣り銭確認',note:'',type:'op'},
  {id:'d3',name:'客席・テーブル消毒',note:'',type:'dy'},
  {id:'d5',name:'施錠・電気・ガス確認',note:'',type:'cl'},
];

/* ============================================================
   買い出しリスト
   ============================================================ */
const BUY_LIST=[
  {cat:'食材',items:[
    {id:'b1',name:'マフィン',qty:'2ストック'},
    {id:'b2',name:'ドッグパン',qty:'3ストック'},
    {id:'b3',name:'食パン',qty:'7ストック'},
    {id:'b4',name:'キャベツ（大）',qty:'2ストック'},
    {id:'b5',name:'リーフレタス',qty:'3ストック'},
    {id:'b6',name:'トマト',qty:'3ストック'},
    {id:'b7',name:'ベーコン',qty:'3ストック'},
    {id:'b8',name:'ドッグソーセージ',qty:'3ストック'},
    {id:'b9',name:'卵',qty:'半分以下→発注',low:true},
  ]},
  {cat:'ドリンク・調味料',items:[
    {id:'b10',name:'紅茶缶',qty:'缶半分→発注',low:true},
    {id:'b11',name:'ミルメーク',qty:'7ストック'},
    {id:'b12',name:'オリーブオイル',qty:'1ストック'},
    {id:'b13',name:'ドレッシング',qty:'1ストック'},
    {id:'b14',name:'マヨネーズ',qty:'1ストック'},
    {id:'b15',name:'ケチャップ',qty:'1ストック'},
    {id:'b16',name:'マスタード',qty:'1ストック'},
    {id:'b17',name:'マーガリン',qty:'1ストック'},
    {id:'b18',name:'シロップ',qty:'1ストック'},
    {id:'b19',name:'グラニュー糖',qty:'1ストック'},
    {id:'b20',name:'ホットコーヒー豆',qty:'1ストック'},
    {id:'b21',name:'アイスコーヒー豆',qty:'1ストック'},
    {id:'b34',name:'コーラ',qty:'1ストック'},
    {id:'b35',name:'牛乳',qty:'3ストック'},
    {id:'b36',name:'オレンジ',qty:'3ストック'},
  ]},
  {cat:'備品・消耗品',items:[
    {id:'b22',name:'おしぼり',qty:'1ストック'},
    {id:'b23',name:'ストロー',qty:'1ストック'},
    {id:'b24',name:'つまようじ',qty:'1ストック'},
    {id:'b25',name:'クイックル',qty:'1ストック'},
    {id:'b26',name:'トイレットペーパー',qty:'1ストック'},
    {id:'b27',name:'消臭剤（手洗い上）',qty:'1ストック'},
    {id:'b28',name:'洗剤',qty:'1ストック'},
    {id:'b29',name:'手袋',qty:'1ストック'},
    {id:'b30',name:'スポンジ',qty:'1ストック'},
    {id:'b31',name:'カナたわし',qty:'1ストック'},
    {id:'b32',name:'アルコール',qty:'1ストック'},
    {id:'b33',name:'ラップ',qty:'1ストック'},
  ]},
];

/* ============================================================
   メニューデータ
   ============================================================ */
const REP_MENU=[
  {cat:'MORNING／モーニング',items:[
    {name:'トーストセット',note:'ドリンク付き',price:550,isSet:true},
    {name:'トーストサンドセット',note:'ドリンク付き',price:650,isSet:true},
    {name:'マフィンセット',note:'ドリンク付き',price:700,isSet:true},
    {name:'ホットドッグセット',note:'ドリンク付き',price:700,isSet:true},
    {name:'トースト',note:'単品',price:500},
    {name:'トーストサンド',note:'単品',price:600},
    {name:'マフィン',note:'単品',price:650},
    {name:'ホットドッグ',note:'単品',price:650},
  ]},
  {cat:'DRINK／ドリンク',items:[
    {name:'コーヒー HOT',note:'',price:500},
    {name:'コーヒー COLD',note:'',price:500},
    {name:'カフェオレ HOT',note:'',price:500},
    {name:'カフェオレ COLD',note:'',price:500},
    {name:'紅茶 ストレート',note:'',price:500},
    {name:'紅茶 レモン',note:'',price:500},
    {name:'紅茶 ミルク',note:'',price:500},
    {name:'ミルメーク',note:'',price:500},
    {name:'コカ・コーラ',note:'',price:500},
    {name:'オレンジジュース',note:'',price:500},
    {name:'ドリンクおかわり',note:'早朝サービス',price:300,isSet:true},
  ]},
  {cat:'SNACK／スナック',items:[
    {name:'煮抜き',note:'ゆで卵',price:100},
  ]},
];
const DRINK_CAT_INDEX=1; // REP_MENU内のDRINKカテゴリのインデックス

/* ============================================================
   初期化
   ============================================================ */
const CHK_SVG=`<svg class="chk-icon" viewBox="0 0 12 12"><polyline points="2,6 5,9 10,3"/></svg>`;
const BDGMAP={op:'b-op',dy:'b-dy',cl:'b-cl'};
const BDGLBL={op:'開店',dy:'毎日',cl:'閉店'};

function init(){
  taskDone = lsGet(SK_TASK);
  buyState  = lsGet(SK_BUY);
  const today=new Date();
  const dj=['日','月','火','水','木','金','土'];
  document.getElementById('hdate').textContent=(today.getMonth()+1)+'月'+today.getDate()+'日（'+dj[today.getDay()]+'）';
  loadDailyInfo();
  renderDailyInfoBanner();
  if(!dailyInfo.staff || !dailyInfo.weather){
    document.getElementById('daily-edit-area').classList.add('open');
    if(dailyInfo.staff) document.getElementById('daily-staff-input').value = dailyInfo.staff;
    dailyEditWeather = dailyInfo.weather || '';
    updateWeatherRadio();
  }
  buildTabs();
  loadPosCarts();
  renderPosTableGrid();
  renderPosMain();
  startSyncPolling();
  syncPullNow();
  if(!getGasUrl()){ updateSyncIndicators(false); }
  // デフォルトで今日の支出日をセット
  const d=new Date();
  const ds=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
  document.getElementById('exp-date').value=ds;
  renderAll();
}

/* ============================================================
   タブ・曜日
   ============================================================ */
function buildTabs(){
  document.getElementById('dtabs').innerHTML=DAYS.map((d,i)=>{
    let cls='dtab';
    if(d===selDay) cls+=' active';
    if(i===todayIdx) cls+=' today-mark';
    return `<button class="${cls}" onclick="changeDay('${d}')">${d}</button>`;
  }).join('');
}
function changeDay(d){ selDay=d; document.querySelectorAll('.dtab').forEach((el,i)=>el.classList.toggle('active',DAYS[i]===d)); renderAll(); }
function renderAll(){ renderTasks(); renderBuy(); }

function switchTab(tab,btn){
  document.querySelectorAll('.tabbtn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById('view-'+tab).classList.add('active');
  const isTask=tab==='tasks';
  document.getElementById('task-header').style.display=isTask?'':'none';
  document.getElementById('dtabs').style.display=isTask?'':'none';
  if(tab==='history') renderHistory();
  if(tab==='expense') renderExpense();
  if(tab==='ai') renderAIWeeks();
  if(tab==='kitchen') renderKitchenList();
  if(tab==='report'){ renderPosTableGrid(); renderPosMain(); }
}

/* ============================================================
   タスク描画
   ============================================================ */
function renderTasks(){
  const el=document.getElementById('view-tasks');
  let tot=0,dn=0,html='';
  html+=`<div class="sec"><div class="sec-lbl">毎日のルーティン</div><div class="card">`;
  DAILY.forEach(t=>{
    const k='d_'+selDay+'_'+t.id, isDone=!!taskDone[k];
    if(isDone)dn++; tot++;
    html+=trowHtml(k,isDone,t.name,t.note,BDGMAP[t.type],BDGLBL[t.type]);
  });
  html+=`</div></div>`;
  const cl=CLEAN[selDay];
  if(cl){
    const k='cl_'+selDay, isDone=!!taskDone[k];
    if(isDone)dn++; tot++;
    html+=`<div class="sec"><div class="sec-lbl">本日の清掃当番</div><div class="card">`;
    html+=trowHtml(k,isDone,cl.name,cl.note,'b-cl2','清掃');
    html+=`</div></div>`;
  }
  const dtasks=DAY_TASKS[selDay]||[];
  if(dtasks.length){
    html+=`<div class="sec"><div class="sec-lbl">${selDay}曜日の固定作業</div><div class="card">`;
    dtasks.forEach(t=>{
      const k='w_'+selDay+'_'+t.id, isDone=!!taskDone[k];
      if(isDone)dn++; tot++;
      html+=trowHtml(k,isDone,t.name,t.note,BDGMAP[t.type],BDGLBL[t.type]);
    });
    html+=`</div></div>`;
  }
  html+=`<div class="task-submit-area">
    <button class="task-submit-btn" onclick="openTaskModal()">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 11.08V12a10 10 0 11-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>
      ${selDay}曜日のタスク完了を報告する
    </button>
  </div>`;
  html+=`<button class="reset-btn" onclick="resetDay()">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><path d="M3.51 15a9 9 0 102.13-9.36L1 10"/></svg>
    ${selDay}曜日のチェックをリセット（記録は履歴に残ります）
  </button>`;
  html+=`<button class="reset-btn" onclick="openTaskHistoryModal()" style="margin-top:6px;">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 8v4l3 3"/><circle cx="12" cy="12" r="9"/></svg>
    タスク完了履歴を見る
  </button>`;
  el.innerHTML=html;
  document.getElementById('prog-num').textContent=dn+'/'+tot;
  const pct=tot?Math.round(dn/tot*100):0;
  document.getElementById('pbar').style.width=pct+'%';
  document.getElementById('prog-pct').textContent=pct+'%';
}

function trowHtml(k,isDone,name,note,badgeCls,badgeLbl){
  return `<div class="trow${isDone?' done':''}" onclick="toggleTask('${k}')">
    <div class="tchk">${CHK_SVG}</div>
    <div class="tinfo"><div class="tlbl">${name}</div>${note?`<div class="tnote">${note}</div>`:''}</div>
    <span class="tbadge ${badgeCls}">${badgeLbl}</span>
  </div>`;
}
function toggleTask(k){ taskDone[k]=!taskDone[k]; renderTasks(); lsSet(SK_TASK,taskDone); }
function resetDay(){
  if(!confirm(selDay+'曜日のチェックをリセットしますか？\n（完了記録は履歴として保存されてから消去されます）'))return;
  const p1='d_'+selDay+'_', p2='cl_'+selDay, p3='w_'+selDay+'_';

  // リセット前に現在の完了状況をスナップショットとして履歴に保存（データは消えない）
  const {tot,dn}=countTaskStatus();
  const now=new Date();
  const dj=['日','月','火','水','木','金','土'];
  const archiveLog=lsGet(SK_TASKLOG,[]);
  archiveLog.push({
    type:'task_reset_archive',
    date:now.toLocaleDateString('ja-JP'),
    youbi:dj[now.getDay()],
    time:now.getHours()+':'+('0'+now.getMinutes()).slice(-2),
    staff:dailyInfo.staff||'未設定',
    taskDay:selDay,
    total:tot,
    done:dn,
    detail:buildTaskSummary(),
    savedAt:now.toISOString()
  });
  lsSet(SK_TASKLOG, archiveLog);

  Object.keys(taskDone).forEach(k=>{if(k.startsWith(p1)||k===p2||k.startsWith(p3)) delete taskDone[k];});
  renderTasks(); lsSet(SK_TASK,taskDone);
  showPosToast(selDay+'曜日のチェックをリセットしました（履歴に記録済み）','ok');
}

/* ============================================================
   ★ タスク完了履歴（閲覧専用・削除不可）
   ============================================================ */
function openTaskHistoryModal(){
  renderTaskHistoryContent();
  document.getElementById('task-history-modal-bg').classList.add('open');
}
function closeTaskHistoryModal(){
  document.getElementById('task-history-modal-bg').classList.remove('open');
}
function renderTaskHistoryContent(){
  const log=lsGet(SK_TASKLOG,[]);
  const el=document.getElementById('task-history-content');
  if(log.length===0){
    el.innerHTML=`<div class="pos-cart-empty">まだタスク完了の記録がありません</div>`;
    return;
  }
  const rows=log.map((h,i)=>({...h,_idx:i})).reverse();
  el.innerHTML=`<div class="form-card">${rows.map(h=>{
    const isReport=h.type!=='task_reset_archive';
    return `<div class="task-hist-row">
      <div class="task-hist-top" style="cursor:pointer;" onclick="toggleTaskHistDetail(${h._idx})">
        <div>
          <span class="task-hist-date">${h.date}（${h.youbi}）${h.taskDay}曜日</span>
          <span class="task-hist-tag ${isReport?'report':'archive'}">${isReport?'完了報告':'リセット時保存'}</span>
        </div>
        <span class="task-hist-progress">${h.done}/${h.total}</span>
      </div>
      <div class="task-hist-staff">${h.time}　担当：${h.staff}</div>
      <div class="task-hist-detail" id="task-hist-detail-${h._idx}">${(h.detail||'').replace(/\n/g,'<br>')}</div>
    </div>`;
  }).join('')}</div>`;
}
function toggleTaskHistDetail(idx){
  const el=document.getElementById('task-hist-detail-'+idx);
  if(el) el.classList.toggle('open');
}

/* ============================================================
   タスク完了モーダル
   ============================================================ */
function buildTaskSummary(){
  const lines=[];
  DAILY.forEach(t=>{ const k='d_'+selDay+'_'+t.id; lines.push((taskDone[k]?'✅ ':'⬜ ')+t.name); });
  const cl=CLEAN[selDay];
  if(cl){ const k='cl_'+selDay; lines.push((taskDone[k]?'✅ ':'⬜ ')+cl.name); }
  (DAY_TASKS[selDay]||[]).forEach(t=>{ const k='w_'+selDay+'_'+t.id; lines.push((taskDone[k]?'✅ ':'⬜ ')+t.name); });
  return lines.join('\n');
}
function countTaskStatus(){
  let tot=0,dn=0;
  DAILY.forEach(t=>{ const k='d_'+selDay+'_'+t.id; tot++; if(taskDone[k])dn++; });
  if(CLEAN[selDay]){ const k='cl_'+selDay; tot++; if(taskDone[k])dn++; }
  (DAY_TASKS[selDay]||[]).forEach(t=>{ const k='w_'+selDay+'_'+t.id; tot++; if(taskDone[k])dn++; });
  return{tot,dn};
}
function openTaskModal(){
  document.getElementById('task-modal-detail').textContent=buildTaskSummary();
  document.getElementById('task-modal-msg').style.display='none';
  document.getElementById('task-modal-bg').classList.add('open');
  if(dailyInfo.staff) document.getElementById('task-staff-input').value=dailyInfo.staff;
}
function closeTaskModal(){ document.getElementById('task-modal-bg').classList.remove('open'); }
async function sendTaskReport(){
  const staff=document.getElementById('task-staff-input').value.trim();
  if(!staff){ showTaskMsg('担当者名を入力してください','err'); return; }
  const {tot,dn}=countTaskStatus();
  const now=new Date();
  const dj=['日','月','火','水','木','金','土'];
  const data={ type:'task', date:now.toLocaleDateString('ja-JP'), youbi:dj[now.getDay()], time:now.getHours()+':'+('0'+now.getMinutes()).slice(-2), staff, taskDay:selDay, total:tot, done:dn, detail:buildTaskSummary() };
  const log=lsGet(SK_TASKLOG,[]);
  log.push({...data, savedAt: now.toISOString()});
  lsSet(SK_TASKLOG, log);
  const gasUrl=getGasUrl();
  if(!gasUrl){ showTaskMsg('✅ 端末に記録しました','ok'); setTimeout(()=>closeTaskModal(),1600); return; }
  showTaskMsg('送信中...','load');
  try{
    await fetch(gasUrl,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(data)});
    showTaskMsg('✅ シートに記録しました！','ok');
    setTimeout(()=>closeTaskModal(),1600);
  }catch(e){
    showTaskMsg('✅ 端末に記録しました\n（シートへの同期は後で確認してください）','ok');
    setTimeout(()=>closeTaskModal(),2200);
  }
}
function showTaskMsg(text,type){
  const el=document.getElementById('task-modal-msg');
  el.textContent=text;
  el.className='msg-box'+(type?' msg-'+type:'');
  el.style.display=text?'block':'none';
}

/* ============================================================
   買い出し描画
   ============================================================ */
function getBuyItem(id){ if(!buyState[id])buyState[id]={bought:false,need:0}; return buyState[id]; }
function renderBuy(){
  const el=document.getElementById('view-buy');
  let boughtCount=0,totalCount=0,needCount=0,html='';
  BUY_LIST.forEach(cat=>{
    html+=`<div class="sec"><div class="sec-lbl">${cat.cat}</div><div class="card">`;
    html+=`<div class="bcat-hd"><span class="bcat-hd-name">商品名</span><span class="bcat-hd-stock">基準</span><span class="bcat-hd-need">今回買う数</span></div>`;
    cat.items.forEach(item=>{
      const st=getBuyItem(item.id);
      totalCount++; if(st.bought)boughtCount++; if(st.need>0)needCount++;
      html+=`<div class="brow${st.bought?' bought':''}">
        <div class="bchk" onclick="toggleBought('${item.id}')">${CHK_SVG}</div>
        <div class="binfo"><span class="bname">${item.name}${item.low?'<span class="blow-tag">要注意</span>':''}</span></div>
        <div class="bstock"><span class="bstock-val">${item.qty}</span></div>
        <div class="bneed">
          <button class="bneed-btn" onclick="changeNeed('${item.id}',-1)">−</button>
          <span class="bneed-val${st.need===0?' zero':''}">${st.need}</span>
          <button class="bneed-btn" onclick="changeNeed('${item.id}',1)">＋</button>
        </div>
      </div>`;
    });
    html+=`</div></div>`;
  });
  const summary=`<div class="sec" style="margin-bottom:.6rem"><div class="card">
    <div class="buy-summary"><span class="buy-sum-lbl">購入済 ${boughtCount}/${totalCount}　｜　要購入 ${needCount}品目</span>
    <span class="buy-sum-num">${needCount>0?needCount+'品目入力中':'未入力'}</span></div>
  </div></div>`;
  const bottom=`<div class="send-area">
    <button class="send-btn" onclick="openSendModal()" ${needCount===0?'disabled':''}>
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
      買い出しリストを送信${needCount>0?' ('+needCount+'品目)':''}
    </button>
  </div>
  <button class="reset-btn" onclick="resetBuy()">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><path d="M3.51 15a9 9 0 102.13-9.36L1 10"/></svg>
    買い出しリストをリセット
  </button>`;
  el.innerHTML=summary+html+bottom;
}
function toggleBought(id){ const st=getBuyItem(id); st.bought=!st.bought; if(st.bought)st.need=0; renderBuy(); lsSet(SK_BUY,buyState); }
function changeNeed(id,delta){ const st=getBuyItem(id); st.need=Math.max(0,st.need+delta); if(st.need>0)st.bought=false; renderBuy(); lsSet(SK_BUY,buyState); }
function resetBuy(){ buyState={}; renderBuy(); lsSet(SK_BUY,buyState); }

/* ============================================================
   買い出し送信モーダル
   ============================================================ */
let sendText='';
function buildSendText(){
  const today=new Date();
  const dj=['日','月','火','水','木','金','土'];
  const dateStr=(today.getMonth()+1)+'月'+today.getDate()+'日（'+dj[today.getDay()]+'）';
  let lines=['【買い出しリスト】 '+dateStr,''];
  let hasItem=false;
  BUY_LIST.forEach(cat=>{
    const targets=cat.items.filter(item=>{const st=getBuyItem(item.id);return st.need>0&&!st.bought;});
    if(targets.length){
      lines.push('■ '+cat.cat);
      targets.forEach(item=>{const st=getBuyItem(item.id);lines.push('  ・'+item.name+'　→ '+st.need+'個'+(item.low?' ⚠要注意':''));hasItem=true;});
      lines.push('');
    }
  });
  if(!hasItem)return null;
  lines.push('以上よろしくお願いします🙏');
  return lines.join('\n');
}
function openSendModal(){
  const text=buildSendText();
  const content=document.getElementById('modal-content');
  const btns=document.getElementById('modal-btns');
  const sub=document.getElementById('modal-sub');
  if(!text){sub.textContent='購入数が入力された商品がありません';content.innerHTML='<div style="padding:20px;text-align:center;color:var(--text3);font-size:13px;">＋ボタンで購入数を入力してください</div>';btns.style.display='none';sendText='';}
  else{
    const cnt=BUY_LIST.flatMap(c=>c.items).filter(i=>getBuyItem(i.id).need>0&&!getBuyItem(i.id).bought).length;
    sub.textContent=cnt+'品目の購入リストを共有できます';
    sendText=text;
    content.innerHTML='<textarea class="modal-ta" id="modal-ta" readonly>'+text+'</textarea>';
    btns.style.display='flex';
  }
  document.getElementById('send-modal-bg').classList.add('open');
}
function closeSendModal(e){if(e&&e.target!==document.getElementById('send-modal-bg'))return;document.getElementById('send-modal-bg').classList.remove('open');}
async function copyList(){
  if(!sendText)return;
  try{await navigator.clipboard.writeText(sendText);const btn=document.querySelector('.modal-copy');btn.textContent='✅ コピーしました';setTimeout(()=>btn.textContent='📋 コピー',2000);}
  catch{const ta=document.getElementById('modal-ta');if(ta){ta.select();document.execCommand('copy');}}
}
function openLine(){if(!sendText)return;window.open('https://line.me/R/msg/text/?'+encodeURIComponent(sendText),'_blank');}

/* ============================================================
   ★ POSレジ
   ============================================================ */
const POS_TABLES=['A','B','C','C2','1','2','3','4','5','6'];
const SK_POS_CARTS='suzu_pos_carts_v1';   // テーブルごとの未会計カート
const SK_KITCHEN='suzu_kitchen_v1';        // キッチン注文履歴
const SK_DAYCLOSE='suzu_dayclose_v1';      // 営業終了サマリー履歴

// カート内部構造: { tableId: { units:[{uid,menuKey,drinkKey}], people, customer } }
// units は1点ずつのユニット配列。セット商品は drinkKey（DRINKカテゴリのmenuKey）を保持。
let posCarts={};
let posSelTable='';
let checkoutSelected={}; // 会計分割用のチェック状態 { uid: bool }
let posUnitSeq=1; // ユニットID発番用
let pendingSetKey=''; // ドリンク選択待ちのセット商品キー

function loadPosCarts(){
  posCarts=lsGet(SK_POS_CARTS,{});
  // 旧データ形式（items:{key:qty}）からの自動移行
  Object.keys(posCarts).forEach(tbl=>{
    const c=posCarts[tbl];
    if(c && !c.units && c.items){
      c.units=[];
      Object.entries(c.items).forEach(([key,qty])=>{
        for(let i=0;i<qty;i++) c.units.push({uid:'u'+(posUnitSeq++),menuKey:key,drinkKey:null});
      });
      delete c.items;
    }
    if(c && !c.units) c.units=[];
  });
}
let savePosCartsDebounceTimer=null;
function savePosCarts(){
  lsSet(SK_POS_CARTS,posCarts);
  // カート変更をサーバーへ送信（連打時はまとめて1回送信）
  if(savePosCartsDebounceTimer) clearTimeout(savePosCartsDebounceTimer);
  savePosCartsDebounceTimer=setTimeout(()=>{ syncPushNow(); },600);
}
function getCart(tbl){
  if(!posCarts[tbl]) posCarts[tbl]={units:[],people:1,customer:''};
  if(!posCarts[tbl].units) posCarts[tbl].units=[];
  return posCarts[tbl];
}
function cartItemCount(tbl){
  const c=posCarts[tbl];
  return c?c.units.length:0;
}
function unitPrice(unit){
  const item=findMenuItemByKey(unit.menuKey);
  return item?item.price:0;
}
function cartTotal(tbl){
  const c=posCarts[tbl];
  if(!c)return 0;
  return c.units.reduce((s,u)=>s+unitPrice(u),0);
}
function findMenuItemByKey(key){
  const [ci,ii]=key.split('_').map(Number);
  return REP_MENU[ci] && REP_MENU[ci].items[ii] ? REP_MENU[ci].items[ii] : null;
}
function menuItemLabel(key){
  const item=findMenuItemByKey(key);
  return item?item.name:'';
}
function unitDisplayName(unit){
  const item=findMenuItemByKey(unit.menuKey);
  if(!item)return'';
  if(item.isSet && unit.drinkKey){
    const drink=findMenuItemByKey(unit.drinkKey);
    return item.name+'（'+(drink?drink.name:'?')+'）';
  }
  if(item.isSet && !unit.drinkKey){
    return item.name+'（ドリンク未選択）';
  }
  return item.name;
}

function renderPosTableGrid(){
  const grid=document.getElementById('pos-table-grid');
  grid.innerHTML=POS_TABLES.map(t=>{
    const cnt=cartItemCount(t);
    let cls='pos-table-btn';
    if(t===posSelTable) cls+=' active';
    else if(cnt>0) cls+=' has-order';
    return `<button class="${cls}" onclick="selectPosTable('${t}')">
      卓${t}
      ${cnt>0?`<span class="pos-table-badge">${cnt}</span>`:''}
    </button>`;
  }).join('');
}

function selectPosTable(tbl){
  posSelTable=tbl;
  renderPosTableGrid();
  renderPosMain();
}

function renderPosMain(){
  const barArea=document.getElementById('pos-current-bar-area');
  const mainArea=document.getElementById('pos-main-area');
  if(!posSelTable){
    barArea.innerHTML='';
    mainArea.innerHTML=`<div style="padding:32px 1rem;text-align:center;color:var(--text3);font-size:13px;">上のテーブルを選んでオーダーを開始してください</div>`;
    return;
  }
  const cart=getCart(posSelTable);
  const cnt=cartItemCount(posSelTable);
  const total=cartTotal(posSelTable);
  barArea.innerHTML=`<div class="pos-current-bar">
    <div><div class="pos-current-tbl">卓${posSelTable} 選択中</div><div class="pos-current-sub">${cnt}点・未確定含む</div></div>
    <div class="pos-current-total">¥${total.toLocaleString()}</div>
  </div>`;

  let html='';
  // メニューパネル（タッチパネル式）
  html+=`<div class="sec"><div class="sec-lbl">メニューをタップして追加</div>`;
  REP_MENU.forEach((cat,ci)=>{
    html+=`<div class="card" style="margin-bottom:8px;">
      <div class="menu-cat-hd" onclick="toggleCat(${ci})">
        <span>${cat.cat}</span><span class="badge" id="cat-badge-${ci}" style="display:none;">0</span>
      </div>
      <div class="menu-items${ci===0?' open':''}" id="cat-items-${ci}" style="padding:10px;">
        <div class="pos-menu-grid">`;
    cat.items.forEach((item,ii)=>{
      const key=ci+'_'+ii;
      const qty=cart.units.filter(u=>u.menuKey===key).length;
      html+=`<button class="pos-menu-btn${qty>0?' in-cart':''}" onclick="posAddItem('${key}')">
        ${qty>0?`<span class="pos-menu-cart-badge">${qty}</span>`:''}
        <span class="pos-menu-name">${item.name}</span>
        <span class="pos-menu-price">${item.note?item.note+' ':''}¥${item.price.toLocaleString()}</span>
      </button>`;
    });
    html+=`</div></div></div>`;
  });
  html+=`</div>`;

  // カート（現在の注文内容）：ユニット単位で表示（セットはドリンク内容も表示）
  html+=`<div class="sec-lbl" style="padding:0 1rem;margin-bottom:.4rem;">卓${posSelTable} の注文内容</div>`;
  if(cart.units.length===0){
    html+=`<div class="pos-cart-card"><div class="pos-cart-empty">まだ注文がありません<br>上のメニューをタップしてください</div></div>`;
  }else{
    html+=`<div class="pos-cart-card">`;
    cart.units.forEach(u=>{
      const item=findMenuItemByKey(u.menuKey);
      if(!item)return;
      const needsDrink=item.isSet && !u.drinkKey;
      html+=`<div class="pos-cart-row">
        <div style="flex:1;">
          <div class="pos-cart-name">${unitDisplayName(u)}${needsDrink?' <span style="color:var(--red);font-size:11px;">⚠未選択</span>':''}</div>
          <div class="pos-cart-price">¥${item.price.toLocaleString()}</div>
        </div>
        ${item.isSet?`<button class="pos-cart-qbtn" style="width:auto;padding:0 8px;font-size:11px;" onclick="openDrinkSelectModal('${u.uid}')">${u.drinkKey?'変更':'選択'}</button>`:''}
        <button class="pos-cart-qbtn" onclick="posRemoveUnit('${u.uid}')">−</button>
        <div class="pos-cart-subtotal">¥${item.price.toLocaleString()}</div>
      </div>`;
    });
    html+=`</div>`;
  }

  // 客層・人数（確定時に記録）
  html+=`<div class="form-row">
    <div class="form-lbl">人数</div>
    <div class="form-card"><div class="num-row">
      <button class="num-btn" onclick="posChangePeople(-1)">−</button>
      <span class="num-val" id="pos-people-val">${cart.people}</span>
      <button class="num-btn" onclick="posChangePeople(1)">＋</button>
      <span style="font-size:13px;color:var(--text2);">名様</span>
    </div></div>
  </div>`;
  html+=`<div class="form-row">
    <div class="form-lbl">客層</div>
    <div class="form-card"><div class="radio-group" id="pos-customer-group">
      ${['常連','新規','観光','ビジネス'].map(c=>`<div class="radio-btn${cart.customer===c?' active':''}" onclick="posSetCustomer('${c}')">${c}</div>`).join('')}
    </div></div>
  </div>`;

  const hasUnselectedDrink=cart.units.some(u=>{const item=findMenuItemByKey(u.menuKey);return item&&item.isSet&&!u.drinkKey;});

  html+=`<button class="pos-confirm-btn" id="pos-confirm-order-btn" onclick="posConfirmOrder()" ${cart.units.length===0||hasUnselectedDrink?'disabled':''}>
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 11.08V12a10 10 0 11-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>
    キッチンに注文を送る
  </button>`;
  if(hasUnselectedDrink){
    html+=`<div style="padding:0 1rem;margin:-4px 0 8px;font-size:11px;color:var(--red);text-align:center;">⚠ セット商品のドリンクを選択してください</div>`;
  }

  html+=`<button class="submit-btn" onclick="openCheckoutModal('${posSelTable}')" ${total===0?'disabled':''} style="background:var(--dark);">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="1" y="4" width="22" height="16" rx="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg>
    お会計する
  </button>`;

  html+=`<button class="reset-btn" onclick="posClearCart('${posSelTable}')">
    <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><path d="M3.51 15a9 9 0 102.13-9.36L1 10"/></svg>
    卓${posSelTable} の注文をクリア
  </button>`;

  mainArea.innerHTML=html;
}

function posAddItem(key){
  if(!posSelTable){ alert('先にテーブルを選択してください'); return; }
  const item=findMenuItemByKey(key);
  if(!item)return;
  if(item.isSet){
    // セット商品はドリンク選択モーダルを開いてから追加する
    pendingSetKey=key;
    openDrinkSelectModal(null);
    return;
  }
  const cart=getCart(posSelTable);
  cart.units.push({uid:'u'+(posUnitSeq++),menuKey:key,drinkKey:null});
  savePosCarts();
  renderPosMain();
  renderPosTableGrid();
}
function posRemoveUnit(uid){
  const cart=getCart(posSelTable);
  cart.units=cart.units.filter(u=>u.uid!==uid);
  savePosCarts();
  renderPosMain();
  renderPosTableGrid();
}
function posChangePeople(d){
  const cart=getCart(posSelTable);
  cart.people=Math.max(1,cart.people+d);
  savePosCarts();
  document.getElementById('pos-people-val').textContent=cart.people;
}
function posSetCustomer(c){
  const cart=getCart(posSelTable);
  cart.customer=c;
  savePosCarts();
  document.querySelectorAll('#pos-customer-group .radio-btn').forEach(b=>b.classList.toggle('active',b.textContent===c));
}
function posClearCart(tbl){
  if(!confirm('卓'+tbl+'の注文内容をすべてクリアしますか？'))return;
  delete posCarts[tbl];
  savePosCarts();
  renderPosMain();
  renderPosTableGrid();
}
function toggleCat(ci){ document.getElementById('cat-items-'+ci).classList.toggle('open'); }

/* ============================================================
   ★ 営業終了・本日の売上サマリー
   ============================================================ */
function todayLocaleDateStr(){ return new Date().toLocaleDateString('ja-JP'); }

function getUnsettledTableCount(){
  return Object.keys(posCarts).filter(t=>posCarts[t] && posCarts[t].units && posCarts[t].units.length>0).length;
}

function buildTodaySummary(){
  const today=todayLocaleDateStr();
  const receipts=lsGet(SK_RECEIPT,[]).filter(r=>r.date===today);
  const totalSales=receipts.reduce((s,r)=>s+r.grand,0);
  const totalGuests=receipts.reduce((s,r)=>s+(r.people||0),0);
  const groups=receipts.length;
  const avgUnit=totalGuests>0?Math.round(totalSales/totalGuests):0;

  // カテゴリ別売上
  const catSales={};
  receipts.forEach(r=>{
    if(!r.order)return;
    r.order.split('/').map(s=>s.trim()).forEach(part=>{
      const m=part.match(/^(.+?)×(\d+)$/);
      if(!m)return;
      const {baseName}=parseOrderPart(m[1]), qty=parseInt(m[2]);
      const menuItem=findMenuItemByName(baseName);
      let cat='その他';
      REP_MENU.forEach(c=>{ if(c.items.find(it=>it.name===baseName)) cat=c.cat.split('／')[0].trim(); });
      catSales[cat]=(catSales[cat]||0)+qty*(menuItem?menuItem.price:0);
    });
  });

  // 客層別売上
  const customerSales={};
  receipts.forEach(r=>{ customerSales[r.customer||'未選択']=(customerSales[r.customer||'未選択']||0)+r.grand; });

  return { date:today, totalSales, groups, totalGuests, avgUnit, catSales, customerSales, staff:dailyInfo.staff, weather:dailyInfo.weather };
}

function openDayCloseModal(){
  const unsettled=getUnsettledTableCount();
  document.getElementById('dayclose-modal-sub').textContent=todayLocaleDateStr()+'　の売上サマリー';
  renderDayCloseContent(unsettled>0);
  document.getElementById('dayclose-modal-bg').classList.add('open');
}
function closeDayCloseModal(){
  document.getElementById('dayclose-modal-bg').classList.remove('open');
}

function renderDayCloseContent(showWarning){
  const s=buildTodaySummary();
  let html='';

  if(showWarning){
    const unsettled=getUnsettledTableCount();
    html+=`<div class="dayclose-warn">⚠️ 未会計のテーブルが ${unsettled}卓 あります（注文がカートに残ったままです）。<br>このまま営業を終了することもできますが、先に会計を済ませることをおすすめします。</div>`;
  }

  html+=`<div class="dayclose-stats-grid">
    <div class="dayclose-stat"><div class="dayclose-stat-lbl">本日売上</div><div class="dayclose-stat-val">¥${s.totalSales.toLocaleString()}</div></div>
    <div class="dayclose-stat"><div class="dayclose-stat-lbl">来店組数</div><div class="dayclose-stat-val">${s.groups}組</div></div>
    <div class="dayclose-stat"><div class="dayclose-stat-lbl">来店人数</div><div class="dayclose-stat-val">${s.totalGuests}名</div></div>
    <div class="dayclose-stat"><div class="dayclose-stat-lbl">客単価</div><div class="dayclose-stat-val">¥${s.avgUnit.toLocaleString()}</div></div>
  </div>`;

  const catEntries=Object.entries(s.catSales).sort((a,b)=>b[1]-a[1]);
  if(catEntries.length){
    const maxCat=Math.max(...catEntries.map(([,v])=>v),1);
    html+=`<div class="dayclose-section-hd">人気カテゴリ別売上</div>`;
    catEntries.forEach(([name,val])=>{
      const pct=Math.round(val/maxCat*100);
      html+=`<div class="dayclose-bar-row">
        <div class="dayclose-bar-lbl">${name}</div>
        <div class="dayclose-bar-track"><div class="dayclose-bar-fill" style="width:${pct}%;"></div></div>
        <div class="dayclose-bar-val">¥${val.toLocaleString()}</div>
      </div>`;
    });
  }

  const custEntries=Object.entries(s.customerSales).sort((a,b)=>b[1]-a[1]);
  if(custEntries.length){
    const maxCust=Math.max(...custEntries.map(([,v])=>v),1);
    html+=`<div class="dayclose-section-hd">客層別売上</div>`;
    custEntries.forEach(([name,val])=>{
      const pct=Math.round(val/maxCust*100);
      html+=`<div class="dayclose-bar-row">
        <div class="dayclose-bar-lbl">${name}</div>
        <div class="dayclose-bar-track"><div class="dayclose-bar-fill" style="width:${pct}%;background:var(--green);"></div></div>
        <div class="dayclose-bar-val">¥${val.toLocaleString()}</div>
      </div>`;
    });
  }

  if(s.groups===0){
    html+=`<div style="padding:20px;text-align:center;color:var(--text3);font-size:13px;">本日の会計データはまだありません</div>`;
  }

  const lineText=buildDayCloseLineText(s);
  html+=`<div class="dayclose-section-hd">LINE共有用テキスト</div>`;
  html+=`<textarea class="dayclose-ta" id="dayclose-ta" readonly>${lineText}</textarea>`;
  html+=`<div class="modal-btns" style="margin-bottom:1rem;">
    <button class="modal-copy" onclick="copyDayCloseText()">📋 コピー</button>
    <button class="modal-line" onclick="openDayCloseLine()">LINE で送る</button>
  </div>`;

  html+=`<div class="msg-box" id="dayclose-msg"></div>`;
  html+=`<button class="submit-btn" style="margin:0 0 .5rem;background:var(--dark);" onclick="confirmDayClose(${showWarning})">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2a10 10 0 100 20A10 10 0 0012 2z"/><path d="M12 7v5l3 3"/></svg>
    営業終了として記録する
  </button>`;

  html+=`<div class="dayclose-section-hd">過去の営業終了履歴</div>`;
  const histList=lsGet(SK_DAYCLOSE,[]);
  if(histList.length===0){
    html+=`<div style="font-size:12px;color:var(--text3);padding:8px 0 16px;">まだ記録がありません</div>`;
  }else{
    html+=`<div class="form-card" style="margin-bottom:1rem;">`;
    histList.slice().reverse().forEach((h,revIdx)=>{
      const idx=histList.length-1-revIdx;
      html+=`<div class="dayclose-history-row clickable" onclick="viewDayCloseHistory(${idx})">
        <span class="dayclose-history-date">${h.date}　${h.groups}組</span>
        <span class="dayclose-history-amt">¥${h.totalSales.toLocaleString()}</span>
      </div>`;
    });
    html+=`</div>`;
  }

  document.getElementById('dayclose-modal-content').innerHTML=html;
}

function buildDayCloseLineText(s){
  const lines=[];
  lines.push('【喫茶すず　本日の売上】 '+s.date);
  if(s.staff) lines.push('担当：'+s.staff+(s.weather?'　天気：'+s.weather:''));
  lines.push('');
  lines.push('売上合計：¥'+s.totalSales.toLocaleString());
  lines.push('来店組数：'+s.groups+'組（'+s.totalGuests+'名様）');
  lines.push('客単価：¥'+s.avgUnit.toLocaleString());
  const catEntries=Object.entries(s.catSales).sort((a,b)=>b[1]-a[1]);
  if(catEntries.length){
    lines.push('');
    lines.push('■ カテゴリ別売上');
    catEntries.forEach(([n,v])=>lines.push('　'+n+'：¥'+v.toLocaleString()));
  }
  const custEntries=Object.entries(s.customerSales).sort((a,b)=>b[1]-a[1]);
  if(custEntries.length){
    lines.push('');
    lines.push('■ 客層別売上');
    custEntries.forEach(([n,v])=>lines.push('　'+n+'：¥'+v.toLocaleString()));
  }
  lines.push('');
  lines.push('本日もお疲れ様でした🌙');
  return lines.join('\n');
}

async function copyDayCloseText(){
  const ta=document.getElementById('dayclose-ta');
  if(!ta)return;
  try{ await navigator.clipboard.writeText(ta.value); const btn=document.querySelector('#dayclose-modal-content .modal-copy'); if(btn){btn.textContent='✅ コピーしました'; setTimeout(()=>btn.textContent='📋 コピー',2000);} }
  catch{ ta.select(); document.execCommand('copy'); }
}
function openDayCloseLine(){
  const ta=document.getElementById('dayclose-ta');
  if(!ta)return;
  window.open('https://line.me/R/msg/text/?'+encodeURIComponent(ta.value),'_blank');
}

function confirmDayClose(hadWarning){
  const s=buildTodaySummary();
  if(s.groups===0){
    if(!confirm('本日の会計データがありません。このまま記録しますか？'))return;
  }
  const unsettled=getUnsettledTableCount();
  if(unsettled>0){
    if(!confirm('未会計のテーブルが'+unsettled+'卓あります。このまま営業終了として記録しますか？'))return;
  }
  const list=lsGet(SK_DAYCLOSE,[]);
  // 同日に既存の記録があれば上書き
  const existingIdx=list.findIndex(h=>h.date===s.date);
  const record={...s, savedAt:new Date().toISOString()};
  if(existingIdx>=0) list[existingIdx]=record;
  else list.push(record);
  lsSet(SK_DAYCLOSE,list);
  showDayCloseMsg('✅ 本日の営業終了を記録しました','ok');
  setTimeout(()=>{ closeDayCloseModal(); },1600);
}
function showDayCloseMsg(text,type){
  const el=document.getElementById('dayclose-msg');
  if(!el)return;
  el.textContent=text;
  el.className='msg-box'+(type?' msg-'+type:'');
  el.style.display=text?'block':'none';
}
function viewDayCloseHistory(idx){
  const list=lsGet(SK_DAYCLOSE,[]);
  const h=list[idx];
  if(!h)return;
  const lines=[
    h.date+' の記録',
    '',
    '売上合計：¥'+h.totalSales.toLocaleString(),
    '来店組数：'+h.groups+'組（'+h.totalGuests+'名様）',
    '客単価：¥'+h.avgUnit.toLocaleString(),
  ];
  alert(lines.join('\n'));
}

/* ============================================================
   ★ ドリンク選択モーダル（セット商品用）
   ============================================================ */
let drinkSelectTargetUid=''; // 既存ユニットのドリンクを変更する場合のuid（新規追加時は空）

function openDrinkSelectModal(uid){
  drinkSelectTargetUid=uid||'';
  let setKey;
  if(uid){
    const cart=getCart(posSelTable);
    const unit=cart.units.find(u=>u.uid===uid);
    if(!unit)return;
    setKey=unit.menuKey;
  }else{
    setKey=pendingSetKey;
  }
  const setItem=findMenuItemByKey(setKey);
  if(!setItem)return;

  document.getElementById('drink-select-sub').textContent=setItem.name+' に付くドリンクを選んでください';
  const drinkCat=REP_MENU[DRINK_CAT_INDEX];
  let html=`<div class="drink-select-set-name">🍽 ${setItem.name}（¥${setItem.price.toLocaleString()}）</div>`;
  html+=`<div class="drink-select-grid">`;
  drinkCat.items.forEach((d,ii)=>{
    if(d.name===setItem.name) return; // 自分自身（例：ドリンクおかわり）は選択肢から除外
    const drinkKey=DRINK_CAT_INDEX+'_'+ii;
    html+=`<button class="drink-select-btn" onclick="confirmDrinkSelect('${setKey}','${drinkKey}')">${d.name}</button>`;
  });
  html+=`</div>`;
  document.getElementById('drink-select-content').innerHTML=html;
  document.getElementById('drink-select-modal-bg').classList.add('open');
}
function closeDrinkSelectModal(){
  document.getElementById('drink-select-modal-bg').classList.remove('open');
  // 新規追加待ちでキャンセルした場合は何も追加しない
  pendingSetKey='';
  drinkSelectTargetUid='';
}
function confirmDrinkSelect(setKey,drinkKey){
  const cart=getCart(posSelTable);
  if(drinkSelectTargetUid){
    // 既存ユニットのドリンクを変更
    const unit=cart.units.find(u=>u.uid===drinkSelectTargetUid);
    if(unit) unit.drinkKey=drinkKey;
  }else{
    // 新規セットをカートに追加
    cart.units.push({uid:'u'+(posUnitSeq++),menuKey:setKey,drinkKey});
  }
  savePosCarts();
  document.getElementById('drink-select-modal-bg').classList.remove('open');
  pendingSetKey='';
  drinkSelectTargetUid='';
  renderPosMain();
  renderPosTableGrid();
}

/* キッチンに注文確定（現在のカート内容をキッチン履歴に積む） */
let posConfirmInProgress=false;
function posConfirmOrder(){
  if(posConfirmInProgress) return; // 連打防止
  const cart=getCart(posSelTable);
  if(cart.units.length===0){ showPosToast('注文内容がありません','err'); return; }
  const hasUnselectedDrink=cart.units.some(u=>{const item=findMenuItemByKey(u.menuKey);return item&&item.isSet&&!u.drinkKey;});
  if(hasUnselectedDrink){ showPosToast('セット商品のドリンクが未選択です','err'); return; }

  posConfirmInProgress=true;
  const btn=document.getElementById('pos-confirm-order-btn');
  if(btn) btn.disabled=true;

  const cnt={};
  cart.units.forEach(u=>{ const n=unitDisplayName(u); cnt[n]=(cnt[n]||0)+1; });
  const itemList=Object.entries(cnt).map(([n,q])=>({name:n,qty:q,served:false}));
  const orderStr=itemList.map(i=>i.name+'×'+i.qty).join(' / ');
  const now=new Date();
  const log=lsGet(SK_KITCHEN,[]);
  log.push({
    table:posSelTable,
    order:orderStr,
    items:itemList,
    time:now.getHours()+':'+('0'+now.getMinutes()).slice(-2),
    date:now.toLocaleDateString('ja-JP'),
    served:false,
    savedAt:now.toISOString()
  });
  lsSet(SK_KITCHEN,log);
  syncPushNow(); // キッチン履歴を即時同期（カートはそのまま・会計のため保持）

  const tbl=posSelTable;
  showPosToast('卓'+tbl+'の注文をキッチンに送信しました','ok');
  renderPosMain();
  renderPosTableGrid();

  // 連打防止は一定時間だけボタンを無効化（カートは消さない）
  setTimeout(()=>{
    posConfirmInProgress=false;
    const btn2=document.getElementById('pos-confirm-order-btn');
    if(btn2) btn2.disabled=false;
  },1200);
}

/* 非ブロッキングのトースト通知（alertの代わり） */
let posToastTimer=null;
function showPosToast(text,type){
  let el=document.getElementById('pos-toast');
  if(!el){
    el=document.createElement('div');
    el.id='pos-toast';
    el.style.position='fixed';
    el.style.bottom='90px';
    el.style.left='50%';
    el.style.transform='translateX(-50%)';
    el.style.maxWidth='360px';
    el.style.width='calc(100% - 2rem)';
    el.style.zIndex='300';
    el.style.padding='12px 16px';
    el.style.borderRadius='10px';
    el.style.fontSize='13px';
    el.style.fontWeight='600';
    el.style.textAlign='center';
    el.style.boxShadow='0 4px 12px rgba(0,0,0,.15)';
    document.body.appendChild(el);
  }
  el.textContent=text;
  el.style.background = type==='err' ? '#FDECEA' : '#EAF3DE';
  el.style.color = type==='err' ? '#C0392B' : '#3B6D11';
  el.style.display='block';
  if(posToastTimer) clearTimeout(posToastTimer);
  posToastTimer=setTimeout(()=>{ el.style.display='none'; },2200);
}

/* ============================================================
   ★ キッチン注文履歴
   ============================================================ */
function renderKitchenList(){
  const log=lsGet(SK_KITCHEN,[]);
  const el=document.getElementById('kitchen-list-area');
  if(log.length===0){
    el.innerHTML=`<div class="kitchen-card"><div class="pos-cart-empty">まだキッチンへの注文はありません</div></div>`;
    return;
  }
  // 旧データ互換：itemsが無い注文はorder文字列から復元
  log.forEach(o=>{
    if(!o.items){
      o.items=(o.order||'').split('/').map(s=>s.trim()).filter(Boolean).map(part=>{
        const m=part.match(/^(.+?)×(\d+)$/);
        return m ? {name:m[1],qty:parseInt(m[2]),served:!!o.served} : {name:part,qty:1,served:!!o.served};
      });
    }
  });

  const rows=log.map((o,i)=>({...o,_idx:i})).reverse();
  // テーブルごとにグループ化（表示順は新しい注文が先頭に来るよう維持）
  const groups=[];
  const groupMap={};
  rows.forEach(o=>{
    if(!groupMap[o.table]){
      groupMap[o.table]={table:o.table, orders:[]};
      groups.push(groupMap[o.table]);
    }
    groupMap[o.table].orders.push(o);
  });

  el.innerHTML=groups.map(g=>{
    const allServed=g.orders.every(o=>o.items.every(it=>it.served));
    return `<div class="kitchen-group${allServed?' all-served':''}">
      <div class="kitchen-group-hd">
        <span class="kitchen-tbl-badge">卓${g.table}</span>
        <span class="kitchen-group-status">${allServed?'✅ 全品提供済':g.orders.length+'件の注文'}</span>
      </div>
      <div class="kitchen-card">
        ${g.orders.map(o=>`
          <div class="kitchen-order-block">
            <div class="kitchen-order-time">${o.time}　送信</div>
            ${o.items.map((it,ii)=>`
              <div class="kitchen-item-row${it.served?' served':''}" onclick="toggleKitchenItemServed(${o._idx},${ii})">
                <div class="kitchen-item-chk${it.served?' checked':''}">${it.served?CHK_SVG:''}</div>
                <div class="kitchen-item-name">${it.name}</div>
                <div class="kitchen-item-qty">×${it.qty}</div>
              </div>
            `).join('')}
          </div>
        `).join('')}
      </div>
    </div>`;
  }).join('');
}

function toggleKitchenItemServed(idx,itemIdx){
  const log=lsGet(SK_KITCHEN,[]);
  if(!log[idx] || !log[idx].items || !log[idx].items[itemIdx])return;
  log[idx].items[itemIdx].served=!log[idx].items[itemIdx].served;
  log[idx].served=log[idx].items.every(it=>it.served); // 全品提供済みなら注文全体も提供済みに
  lsSet(SK_KITCHEN,log);
  renderKitchenList();
  syncPushNow();
}
function clearServedKitchen(){
  let log=lsGet(SK_KITCHEN,[]);
  const before=log.length;
  log=log.filter(o=>{
    const items=o.items||[];
    const allServed=items.length>0 ? items.every(it=>it.served) : !!o.served;
    return !allServed;
  });
  lsSet(SK_KITCHEN,log);
  renderKitchenList();
  if(before!==log.length){ syncPushNow(); }
}

/* ============================================================
   ★ 会計（チェックアウト）モーダル：分割対応＋お預かり計算
   ============================================================ */
let checkoutTable='';

function openCheckoutModal(tbl){
  checkoutTable=tbl;
  const cart=getCart(tbl);
  if(cart.units.length===0){ alert('注文内容がありません'); return; }
  // 全品目をデフォルトで選択状態に
  checkoutSelected={};
  cart.units.forEach(u=>{ checkoutSelected[u.uid]=true; });

  document.getElementById('checkout-modal-sub').textContent='卓'+tbl+'　全'+cart.units.length+'点';
  renderCheckoutModalContent();
  document.getElementById('checkout-modal-bg').classList.add('open');
}
function closeCheckoutModal(){
  document.getElementById('checkout-modal-bg').classList.remove('open');
}

function expandCartUnits(tbl){
  // チェックアウト用にカートのユニットへ表示名・金額を付与して返す
  const cart=getCart(tbl);
  return cart.units.map(u=>({
    unitKey:u.uid,
    menuKey:u.menuKey,
    name:unitDisplayName(u),
    price:unitPrice(u)
  }));
}

function renderCheckoutModalContent(){
  const units=expandCartUnits(checkoutTable);
  const selectedUnits=units.filter(u=>checkoutSelected[u.unitKey]);
  const grand=selectedUnits.reduce((s,u)=>s+u.price,0); // 表示金額＝税込。これをそのまま受け取る
  const taxIncluded=Math.round(grand-grand/1.1); // 内税額（参考表示のみ）

  let html=`<div class="pos-split-toolbar">
    <button class="pos-split-btn" onclick="checkoutSelectAll(true)">全選択</button>
    <button class="pos-split-btn" onclick="checkoutSelectAll(false)">全解除</button>
  </div>`;

  html+=`<div class="pos-checkout-card">`;
  units.forEach(u=>{
    const checked=!!checkoutSelected[u.unitKey];
    html+=`<div class="pos-checkout-row" onclick="toggleCheckoutUnit('${u.unitKey}')">
      <div class="pos-checkout-chk${checked?' checked':''}">${checked?CHK_SVG:''}</div>
      <div class="pos-checkout-name">${u.name}</div>
      <div class="pos-checkout-amt">¥${u.price.toLocaleString()}</div>
    </div>`;
  });
  html+=`</div>`;

  html+=`<div class="total-panel" style="margin:0 0 1rem;">
    <div class="total-row"><span>内消費税（10%・参考）</span><span>¥${taxIncluded.toLocaleString()}</span></div>
    <div class="total-grand"><span>ご請求金額（税込）</span><span>¥${grand.toLocaleString()}</span></div>
  </div>`;

  // お預かり・おつり
  html+=`<div class="form-card" style="margin-bottom:1rem;">
    <div class="field-wrap"><span class="field-lbl">お預かり金額</span></div>
    <div class="cash-row">
      <input type="number" class="cash-input" id="checkout-cash-input" placeholder="0" min="0" oninput="updateChangeDisplay(${grand})">
      <span style="font-size:13px;color:var(--text2);">円</span>
    </div>
    <div class="cash-quick-row">
      ${[1000,2000,5000,10000].map(v=>`<button class="cash-quick-btn" onclick="setCheckoutCash(${v},${grand})">¥${v.toLocaleString()}</button>`).join('')}
      <button class="cash-quick-btn" onclick="setCheckoutCash(${grand},${grand})">ぴったり</button>
    </div>
    <div class="change-display">
      <span class="change-lbl">おつり</span>
      <span class="change-val" id="checkout-change-val">¥0</span>
    </div>
  </div>`;

  html+=`<div class="msg-box" id="checkout-msg"></div>`;
  html+=`<button class="submit-btn" style="margin:0 0 .5rem;" onclick="finalizeCheckout()">
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21H5a2 2 0 01-2-2V5a2 2 0 012-2h11l5 5v13a2 2 0 01-2 2z"/><polyline points="17 21 17 13 7 13"/><polyline points="7 3 7 8 15 8"/></svg>
    選択分の会計を確定する
  </button>`;

  document.getElementById('checkout-modal-content').innerHTML=html;
}

function toggleCheckoutUnit(unitKey){
  checkoutSelected[unitKey]=!checkoutSelected[unitKey];
  renderCheckoutModalContent();
}
function checkoutSelectAll(val){
  const units=expandCartUnits(checkoutTable);
  units.forEach(u=>{ checkoutSelected[u.unitKey]=val; });
  renderCheckoutModalContent();
}
function setCheckoutCash(v,grand){
  document.getElementById('checkout-cash-input').value=v;
  updateChangeDisplay(grand);
}
function updateChangeDisplay(grand){
  const cash=parseInt(document.getElementById('checkout-cash-input').value)||0;
  const change=cash-grand;
  const el=document.getElementById('checkout-change-val');
  el.textContent='¥'+Math.abs(change).toLocaleString();
  el.className='change-val'+(change<0?' negative':'');
  if(change<0) el.textContent='不足 '+el.textContent;
}

async function finalizeCheckout(){
  const units=expandCartUnits(checkoutTable);
  const selectedUnits=units.filter(u=>checkoutSelected[u.unitKey]);
  if(selectedUnits.length===0){ showCheckoutMsg('会計する品目を選択してください','err'); return; }

  const grand=selectedUnits.reduce((s,u)=>s+u.price,0); // 表示金額＝税込でそのまま受け取る
  const taxIncluded=Math.round(grand-grand/1.1); // 内税額（記録用の参考値）
  const sub=grand-taxIncluded; // 税抜換算（記録用の参考値）
  const cart=getCart(checkoutTable);
  const staff=dailyInfo.staff, weather=dailyInfo.weather;

  if(!staff||!weather){
    showCheckoutMsg('「本日の固定情報」（担当者・天気）を会計入力タブで設定してください','err');
    return;
  }

  // 注文文字列（選択分のみ、表示名ごとに集計）
  const cnt={};
  selectedUnits.forEach(u=>{ cnt[u.name]=(cnt[u.name]||0)+1; });
  const orderStr=Object.entries(cnt).map(([n,q])=>n+'×'+q).join(' / ');

  const now=new Date();
  const dj=['日','月','火','水','木','金','土'];
  const data={
    type:'receipt', date:now.toLocaleDateString('ja-JP'), youbi:dj[now.getDay()],
    time:now.getHours()+':'+('0'+now.getMinutes()).slice(-2), staff,
    table:checkoutTable, people:cart.people||1, customer:cart.customer||'未選択', weather,
    timeIn:now.getHours()+':'+('0'+now.getMinutes()).slice(-2), timeOut:'', order:orderStr, subtotal:sub, tax:taxIncluded, grand,
    unitPrice:cart.people>0?Math.floor(grand/cart.people):grand, memo:'なし', savedAt:now.toISOString()
  };
  const receipts=lsGet(SK_RECEIPT,[]);
  receipts.push(data);
  lsSet(SK_RECEIPT,receipts);

  // 会計済みユニットをカートから除去（残りは引き続き未会計として保持＝テーブル会計分割対応）
  const selectedUidSet=new Set(selectedUnits.map(u=>u.unitKey));
  cart.units=cart.units.filter(u=>!selectedUidSet.has(u.uid));
  if(cart.units.length===0){ delete posCarts[checkoutTable]; }
  savePosCarts();

  showCheckoutMsg('保存中...','load');
  const gasUrl=getGasUrl();
  const doFinish=(msg)=>{
    showCheckoutMsg(msg,'ok');
    setTimeout(()=>{
      closeCheckoutModal();
      renderPosMain();
      renderPosTableGrid();
    },1800);
  };
  if(!gasUrl){ doFinish('✅ ¥'+grand.toLocaleString()+' お会計しました'); return; }
  try{
    const res=await fetch(gasUrl,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(data)});
    const json=await res.json();
    if(json.status==='ok') doFinish('✅ ¥'+grand.toLocaleString()+' シートに保存しました');
    else doFinish('⚠ シートエラーですが端末には保存済みです');
  }catch(e){
    doFinish('✅ ¥'+grand.toLocaleString()+' 保存しました（シート同期は後で確認）');
  }
}
function showCheckoutMsg(text,type){
  const el=document.getElementById('checkout-msg');
  if(!el)return;
  el.textContent=text;
  el.className='msg-box'+(type?' msg-'+type:'');
  el.style.display=text?'block':'none';
}

/* ============================================================
   ★ 会計履歴 + 個別削除
   ============================================================ */
let histSelDate='';
let pendingDeleteIdx=-1;

function renderHistory(){
  const receipts=lsGet(SK_RECEIPT,[]);
  const el=document.getElementById('hist-content');
  const filterEl=document.getElementById('hist-date-filter');
  const dayTotalEl=document.getElementById('hist-day-total');

  if(receipts.length===0){
    filterEl.innerHTML='';
    dayTotalEl.style.display='none';
    el.innerHTML=`<div class="hist-card"><div class="hist-empty">まだ会計データがありません<br>「会計入力」タブから保存してください</div></div>`;
    return;
  }
  const dates=[...new Set(receipts.map(r=>r.date))].reverse();
  if(!histSelDate||!dates.includes(histSelDate)) histSelDate=dates[0];
  filterEl.innerHTML=dates.map(d=>`<button class="date-tab${d===histSelDate?' active':''}" onclick="histSelectDate('${d}')">${d.replace(/\d{4}\//,'')}</button>`).join('');

  const dayReceipts=receipts.map((r,i)=>({...r,_origIdx:i})).filter(r=>r.date===histSelDate).reverse();
  const dayTotal=dayReceipts.reduce((s,r)=>s+r.grand,0);
  dayTotalEl.style.display='flex';
  document.getElementById('hist-day-total-val').textContent='¥'+dayTotal.toLocaleString();
  document.getElementById('hist-day-count').textContent=dayReceipts.length+'件';

  if(dayReceipts.length===0){
    el.innerHTML=`<div class="hist-card"><div class="hist-empty">この日の会計データはありません</div></div>`;
    return;
  }
  let html='<div class="hist-header"><span class="hist-title">明細</span><span style="font-size:11px;color:var(--text3);">新しい順 ╱ ✕で取り消し</span></div>';
  html+='<div class="hist-card">';
  dayReceipts.forEach(r=>{
    html+=`<div class="hist-row">
      <div class="hist-time">${r.time}<br>卓${r.table}<br>${r.people}名</div>
      <div class="hist-info">
        <div class="hist-tbl">${r.customer} ${r.weather?'/ '+r.weather:''}</div>
        <div class="hist-order">${r.order||'—'}</div>
        ${r.memo&&r.memo!=='なし'?`<div class="hist-order" style="color:var(--br);margin-top:2px;">📝 ${r.memo}</div>`:''}
      </div>
      <div style="text-align:right;min-width:70px;">
        <div class="hist-amt">¥${r.grand.toLocaleString()}</div>
        <div class="hist-staff">${r.staff}</div>
      </div>
      <button class="hist-del-btn" onclick="confirmDelete(${r._origIdx})" title="取り消し">✕</button>
    </div>`;
  });
  html+='</div>';

  const allTotal=receipts.reduce((s,r)=>s+r.grand,0);
  html+=`<div style="padding:0 1rem;margin-bottom:.5rem;">
    <div style="background:var(--cream);border-radius:10px;padding:10px 14px;display:flex;justify-content:space-between;align-items:center;">
      <div style="font-size:11px;color:var(--text3);">累計売上（全期間・${receipts.length}件）</div>
      <div style="font-size:16px;font-weight:700;color:var(--br);">¥${allTotal.toLocaleString()}</div>
    </div>
  </div>`;
  const gasUrl=getGasUrl();
  html+=`<div style="padding:0 1rem;margin-bottom:1rem;">
    <button class="reset-btn" onclick="openGasModal()" style="width:100%;margin:0;">
      ⚙️ GAS URL設定（シート連携）　${gasUrl?'✅ 設定済':'未設定'}
    </button>
  </div>`;
  el.innerHTML=html;
}
function histSelectDate(d){ histSelDate=d; renderHistory(); }

function confirmDelete(idx){
  const receipts=lsGet(SK_RECEIPT,[]);
  const r=receipts[idx];
  if(!r)return;
  pendingDeleteIdx=idx;
  document.getElementById('confirm-modal-detail').innerHTML=
    `日時: ${r.date} ${r.time}<br>卓: ${r.table}番 / ${r.people}名様<br>注文: ${r.order}<br>金額: ¥${r.grand.toLocaleString()}`;
  document.getElementById('confirm-modal-bg').classList.add('open');
}
function closeConfirmModal(){ pendingDeleteIdx=-1; document.getElementById('confirm-modal-bg').classList.remove('open'); }
function executeDelete(){
  if(pendingDeleteIdx<0)return;
  const receipts=lsGet(SK_RECEIPT,[]);
  receipts.splice(pendingDeleteIdx,1);
  lsSet(SK_RECEIPT,receipts);
  closeConfirmModal();
  renderHistory();
}

/* ============================================================
   ★ 経費・支出管理
   ============================================================ */
let expCat='';
let expSelYear='';

function setExpCat(v){
  expCat=v;
  document.querySelectorAll('#exp-cat-group .radio-btn').forEach(b=>b.classList.toggle('active',b.textContent===v));
}

function submitExpense(){
  const date=document.getElementById('exp-date').value;
  const name=document.getElementById('exp-name').value.trim();
  const amount=parseInt(document.getElementById('exp-amount').value)||0;
  const receiptNo=document.getElementById('exp-receipt-no').value.trim();
  const msgEl=document.getElementById('exp-msg');
  if(!date){ showExpMsg('支出日を入力してください','err'); return; }
  if(!expCat){ showExpMsg('カテゴリを選択してください','err'); return; }
  if(!name){ showExpMsg('内容を入力してください','err'); return; }
  if(amount<=0){ showExpMsg('金額を正しく入力してください','err'); return; }
  const exp={ date, cat:expCat, name, amount, receiptNo, savedAt:new Date().toISOString() };
  const exps=lsGet(SK_EXPENSE,[]);
  exps.push(exp);
  lsSet(SK_EXPENSE,exps);
  document.getElementById('exp-name').value='';
  document.getElementById('exp-amount').value='';
  document.getElementById('exp-receipt-no').value='';
  expCat='';
  document.querySelectorAll('#exp-cat-group .radio-btn').forEach(b=>b.classList.remove('active'));
  showExpMsg('✅ 経費を登録しました（¥'+amount.toLocaleString()+'）','ok');
  setTimeout(()=>showExpMsg('',''),2500);
  renderExpense();
}
function showExpMsg(text,type){
  const el=document.getElementById('exp-msg');
  el.textContent=text;
  el.className='msg-box'+(type?' msg-'+type:'');
  el.style.display=text?'block':'none';
}
function deleteExpense(idx){
  if(!confirm('この経費を削除しますか？'))return;
  const exps=lsGet(SK_EXPENSE,[]);
  exps.splice(idx,1);
  lsSet(SK_EXPENSE,exps);
  renderExpense();
}
function renderExpense(){
  const exps=lsGet(SK_EXPENSE,[]);
  const years=[...new Set(exps.map(e=>e.date.slice(0,4)))].sort().reverse();
  const yearFilterEl=document.getElementById('exp-year-filter');
  const listEl=document.getElementById('exp-list-area');
  const taxEl=document.getElementById('tax-summary-area');

  if(!expSelYear||!years.includes(expSelYear)) expSelYear=years[0]||(new Date().getFullYear()+'');
  yearFilterEl.innerHTML=years.map(y=>`<button class="tax-year-tab${y===expSelYear?' active':''}" onclick="expSelectYear('${y}')">${y}年</button>`).join('')||'<span style="font-size:12px;color:var(--text3);padding:0 1rem;">登録データなし</span>';

  const yearExps=exps.map((e,i)=>({...e,_origIdx:i})).filter(e=>e.date.startsWith(expSelYear)).sort((a,b)=>b.date.localeCompare(a.date));
  const catMap={'食材・仕入':'exp-food','光熱費':'exp-util','消耗品':'exp-supply','その他':'exp-other'};

  if(yearExps.length===0){
    listEl.innerHTML=`<div style="padding:0 1rem 1rem"><div class="form-card"><div class="hist-empty">この年の経費データはありません</div></div></div>`;
  }else{
    let html=`<div style="padding:0 1rem;margin-bottom:.5rem;"><div class="form-lbl">${expSelYear}年の経費一覧</div></div>`;
    html+=`<div style="padding:0 1rem;margin-bottom:1rem;"><div class="form-card">`;
    yearExps.forEach(e=>{
      const cls=catMap[e.cat]||'exp-other';
      html+=`<div class="exp-row">
        <button class="exp-del-btn" onclick="deleteExpense(${e._origIdx})" title="削除">✕</button>
        <div class="exp-info">
          <div class="exp-name">${e.name}</div>
          <div class="exp-meta">${e.date}　${e.receiptNo?'領収書: '+e.receiptNo:''}</div>
        </div>
        <div style="text-align:right;flex-shrink:0;">
          <div class="exp-amt">¥${e.amount.toLocaleString()}</div>
          <span class="exp-cat-badge ${cls}">${e.cat}</span>
        </div>
      </div>`;
    });
    html+=`</div></div>`;
    listEl.innerHTML=html;
  }

  // 確定申告サマリ
  renderTaxSummary(exps,yearExps,expSelYear,taxEl);
}
function expSelectYear(y){ expSelYear=y; renderExpense(); }

function renderTaxSummary(allExps,yearExps,year,el){
  const receipts=lsGet(SK_RECEIPT,[]);
  const yearReceipts=receipts.filter(r=>{
    const ry=r.date.split('/')[0]||r.date.slice(0,4);
    return ry===year;
  });
  const totalSales=yearReceipts.reduce((s,r)=>s+r.grand,0);
  const taxIncSales=Math.round(totalSales/1.1);
  const totalExpense=yearExps.reduce((s,e)=>s+e.amount,0);
  const profit=totalSales-totalExpense;

  const catTotals={};
  yearExps.forEach(e=>{ catTotals[e.cat]=(catTotals[e.cat]||0)+e.amount; });

  const months={};
  yearExps.forEach(e=>{
    const m=e.date.slice(0,7);
    months[m]=(months[m]||0)+e.amount;
  });

  el.innerHTML=`<div class="tax-panel">
    <div class="tax-section-hd">📊 ${year}年 確定申告サマリ</div>
    <div class="tax-row"><span class="tax-lbl">売上合計（税込）</span><span class="tax-val">¥${totalSales.toLocaleString()}</span></div>
    <div class="tax-row"><span class="tax-lbl">売上合計（税抜換算）</span><span class="tax-val">¥${taxIncSales.toLocaleString()}</span></div>
    <div class="tax-row"><span class="tax-lbl">経費合計</span><span class="tax-val" style="color:#FF8A80;">¥${totalExpense.toLocaleString()}</span></div>
    <div class="tax-row" style="border-top:1px solid #5c3a1e;padding-top:10px;margin-top:6px;">
      <span class="tax-lbl" style="font-size:15px;font-weight:700;">概算利益</span>
      <span class="tax-profit">¥${profit.toLocaleString()}</span>
    </div>
    <div class="tax-section-hd" style="margin-top:16px;">カテゴリ別 経費内訳</div>
    ${Object.entries(catTotals).map(([c,v])=>`<div class="tax-row"><span class="tax-lbl">${c}</span><span class="tax-val">¥${v.toLocaleString()}</span></div>`).join('')||'<div style="font-size:12px;color:var(--bl);">経費データなし</div>'}
  </div>`;
}

/* ============================================================
   ★ AI 売上分析
   ============================================================ */
let aiSelWeek='';
let aiWeeks=[];

function getWeekKey(dateStr){
  const d=new Date(dateStr.replace(/\//g,'-').replace(/(\d+)年(\d+)月(\d+)日.*$/,'$1-$2-$3'));
  if(isNaN(d))return null;
  const day=d.getDay();
  const mon=new Date(d); mon.setDate(d.getDate()-(day===0?6:day-1));
  return mon.getFullYear()+'-'+String(mon.getMonth()+1).padStart(2,'0')+'-'+String(mon.getDate()).padStart(2,'0');
}
function weekLabel(key){
  const d=new Date(key);
  const end=new Date(d); end.setDate(d.getDate()+6);
  const f=x=>(x.getMonth()+1)+'/'+(x.getDate());
  return f(d)+'〜'+f(end);
}

function renderAIWeeks(){
  const receipts=lsGet(SK_RECEIPT,[]);
  const weekSet=new Set();
  receipts.forEach(r=>{ const k=getWeekKey(r.date); if(k)weekSet.add(k); });
  aiWeeks=[...weekSet].sort().reverse();
  if(!aiSelWeek||!aiWeeks.includes(aiSelWeek)) aiSelWeek=aiWeeks[0]||'';

  const sel=document.getElementById('ai-week-selector');
  if(aiWeeks.length===0){
    sel.innerHTML='<span style="font-size:12px;color:var(--text3);padding:0 1rem;">データなし</span>';
    document.getElementById('ai-stats-grid').innerHTML='';
    document.getElementById('ai-result-area').innerHTML='';
    return;
  }
  sel.innerHTML=aiWeeks.map(w=>`<button class="ai-week-tab${w===aiSelWeek?' active':''}" onclick="aiSelectWeek('${w}')">${weekLabel(w)}</button>`).join('');
  renderAIStats();
}
function aiSelectWeek(w){
  aiSelWeek=w;
  document.querySelectorAll('.ai-week-tab').forEach(b=>b.classList.toggle('active',b.textContent===weekLabel(w)));
  document.getElementById('ai-result-area').innerHTML='';
  renderAIStats();
}

function getWeekReceipts(){
  const receipts=lsGet(SK_RECEIPT,[]);
  return receipts.filter(r=>getWeekKey(r.date)===aiSelWeek);
}

function renderAIStats(){
  const wr=getWeekReceipts();
  const totalSales=wr.reduce((s,r)=>s+r.grand,0);
  const totalGuests=wr.reduce((s,r)=>s+r.people,0);
  const avgUnit=wr.length>0?Math.round(totalSales/totalGuests):0;
  const groups=wr.length;

  document.getElementById('ai-stats-grid').innerHTML=`
    <div class="ai-stat-card"><div class="ai-stat-lbl">週間売上</div><div class="ai-stat-val">¥${totalSales.toLocaleString()}</div><div class="ai-stat-sub">${weekLabel(aiSelWeek)}</div></div>
    <div class="ai-stat-card"><div class="ai-stat-lbl">来店組数</div><div class="ai-stat-val">${groups}組</div><div class="ai-stat-sub">合計${totalGuests}名様</div></div>
    <div class="ai-stat-card"><div class="ai-stat-lbl">客単価（平均）</div><div class="ai-stat-val">¥${avgUnit.toLocaleString()}</div><div class="ai-stat-sub">1名あたり</div></div>
    <div class="ai-stat-card"><div class="ai-stat-lbl">1日平均売上</div><div class="ai-stat-val">¥${Math.round(totalSales/7).toLocaleString()}</div><div class="ai-stat-sub">週7日換算</div></div>
  `;

  renderMenuChart(wr);
  renderHourChart(wr);
  renderCustomerChart(wr);
}

function renderBarChart(items, containerId){
  const maxVal=Math.max(...items.map(i=>i.val),1);
  const bars=items.map(i=>{
    const h=Math.max(4,Math.round((i.val/maxVal)*90));
    return `<div class="bar-item">
      <div style="font-size:9px;color:var(--text3);margin-bottom:2px;">¥${i.val>0?Math.round(i.val/1000)+'k':'0'}</div>
      <div class="bar-fill" style="height:${h}px;"></div>
      <div class="bar-lbl">${i.lbl}</div>
    </div>`;
  }).join('');
  document.getElementById(containerId).innerHTML=`<div class="bar-chart">${bars}</div>`;
}

function parseOrderPart(name){
  // 'セット名（ドリンク名）' 形式から実際の商品名を取り出す（セット本体の名前を返す）
  const m=name.match(/^(.+?)（(.+)）$/);
  if(m) return {baseName:m[1], drinkName:m[2]};
  return {baseName:name, drinkName:null};
}
function findMenuItemByName(name){
  return REP_MENU.flatMap(c=>c.items).find(it=>it.name===name)||null;
}

function renderMenuChart(wr){
  const catSales={};
  wr.forEach(r=>{
    if(!r.order)return;
    r.order.split('/').map(s=>s.trim()).forEach(part=>{
      const m=part.match(/^(.+?)×(\d+)$/);
      if(!m)return;
      const {baseName}=parseOrderPart(m[1]), qty=parseInt(m[2]);
      const menuItem=findMenuItemByName(baseName);
      let cat='その他';
      REP_MENU.forEach(c=>{ if(c.items.find(it=>it.name===baseName)) cat=c.cat.split('／')[0].trim(); });
      catSales[cat]=(catSales[cat]||0)+qty*(menuItem?menuItem.price:0);
    });
  });
  const items=Object.entries(catSales).map(([lbl,val])=>({lbl,val})).sort((a,b)=>b.val-a.val);
  document.getElementById('ai-menu-chart').innerHTML=items.length?`<div class="bar-chart">${items.map(i=>{const max=Math.max(...items.map(x=>x.val),1);const h=Math.max(4,Math.round((i.val/max)*90));return `<div class="bar-item"><div style="font-size:9px;color:var(--text3);margin-bottom:2px;">¥${Math.round(i.val/1000)}k</div><div class="bar-fill" style="height:${h}px;"></div><div class="bar-lbl" style="font-size:8px;">${i.lbl}</div></div>`}).join('')}</div>`:'<div style="font-size:12px;color:var(--text3);text-align:center;padding:16px;">データなし</div>';
}

function renderHourChart(wr){
  const slots={'7-9':0,'9-11':0,'11-13':0,'13-15':0,'15-17':0};
  wr.forEach(r=>{
    if(!r.timeIn)return;
    const h=parseInt(r.timeIn.split(':')[0]);
    if(h>=7&&h<9) slots['7-9']++;
    else if(h>=9&&h<11) slots['9-11']++;
    else if(h>=11&&h<13) slots['11-13']++;
    else if(h>=13&&h<15) slots['13-15']++;
    else if(h>=15&&h<17) slots['15-17']++;
  });
  const items=Object.entries(slots).map(([lbl,val])=>({lbl,val}));
  const max=Math.max(...items.map(i=>i.val),1);
  document.getElementById('ai-hour-chart').innerHTML=`<div class="bar-chart">${items.map(i=>{const h=Math.max(4,Math.round((i.val/max)*90));return `<div class="bar-item"><div style="font-size:9px;color:var(--text3);margin-bottom:2px;">${i.val}組</div><div class="bar-fill" style="height:${h}px;background:#C8956C;"></div><div class="bar-lbl">${i.lbl}</div></div>`}).join('')}</div>`;
}

function renderCustomerChart(wr){
  const cats={};
  wr.forEach(r=>{ cats[r.customer]=(cats[r.customer]||0)+r.grand; });
  const items=Object.entries(cats).map(([lbl,val])=>({lbl,val})).sort((a,b)=>b.val-a.val);
  const max=Math.max(...items.map(i=>i.val),1);
  document.getElementById('ai-customer-chart').innerHTML=items.length?`<div class="bar-chart">${items.map(i=>{const h=Math.max(4,Math.round((i.val/max)*90));return `<div class="bar-item"><div style="font-size:9px;color:var(--text3);margin-bottom:2px;">¥${Math.round(i.val/1000)}k</div><div class="bar-fill" style="height:${h}px;background:#3B6D11;"></div><div class="bar-lbl">${i.lbl}</div></div>`}).join('')}</div>`:'<div style="font-size:12px;color:var(--text3);text-align:center;padding:16px;">データなし</div>';
}

async function generateAIAnalysis(){
  const wr=getWeekReceipts();
  if(wr.length===0){ alert('この週の会計データがありません'); return; }

  const btn=document.getElementById('ai-gen-btn');
  btn.disabled=true;
  btn.textContent='分析中...';
  document.getElementById('ai-result-area').innerHTML='<div class="ai-result-box loading">✨ AI が売上データを分析しています...</div>';

  const totalSales=wr.reduce((s,r)=>s+r.grand,0);
  const totalGuests=wr.reduce((s,r)=>s+r.people,0);
  const avgUnit=wr.length>0?Math.round(totalSales/totalGuests):0;

  const menuCount={};
  const drinkCount={};
  wr.forEach(r=>{
    if(!r.order)return;
    r.order.split('/').map(s=>s.trim()).forEach(part=>{
      const m=part.match(/^(.+?)×(\d+)$/);
      if(!m)return;
      const {baseName,drinkName}=parseOrderPart(m[1]), qty=parseInt(m[2]);
      menuCount[baseName]=(menuCount[baseName]||0)+qty;
      if(drinkName) drinkCount[drinkName]=(drinkCount[drinkName]||0)+qty;
    });
  });
  const topMenu=Object.entries(menuCount).sort((a,b)=>b[1]-a[1]).slice(0,5).map(([n,c])=>n+'×'+c+'件').join('、');
  const topDrink=Object.entries(drinkCount).sort((a,b)=>b[1]-a[1]).slice(0,5).map(([n,c])=>n+'×'+c+'件').join('、');

  const catSales={};
  wr.forEach(r=>{ catSales[r.customer]=(catSales[r.customer]||0)+r.grand; });
  const customerStr=Object.entries(catSales).map(([c,v])=>c+'：¥'+v.toLocaleString()).join('、');

  const hourSlots={};
  wr.forEach(r=>{
    if(!r.timeIn)return;
    const h=parseInt(r.timeIn.split(':')[0])+'時台';
    hourSlots[h]=(hourSlots[h]||0)+1;
  });
  const hourStr=Object.entries(hourSlots).sort((a,b)=>b[1]-a[1]).map(([h,c])=>h+c+'組').join('、');

  const exps=lsGet(SK_EXPENSE,[]);
  const weekExps=exps.filter(e=>getWeekKey(e.date)===aiSelWeek);
  const totalExp=weekExps.reduce((s,e)=>s+e.amount,0);

  const prompt=`あなたは小さな喫茶店「喫茶すず」の経営コンサルタントです。以下の週次データを分析し、売上向上のための具体的な提案を日本語で行ってください。

【対象週】${weekLabel(aiSelWeek)}
【売上合計】¥${totalSales.toLocaleString()}
【来店組数】${wr.length}組・合計${totalGuests}名
【客単価】¥${avgUnit.toLocaleString()}/名
【人気メニュートップ5】${topMenu||'データなし'}
【セット注文時の人気ドリンクトップ5】${topDrink||'データなし'}
【客層別売上】${customerStr||'データなし'}
【混雑時間帯】${hourStr||'データなし'}
【今週経費】¥${totalExp.toLocaleString()}

以下の4つの観点で分析してください（各200字程度）：
1. 【今週の成果と課題】売上・客単価・来客数の評価
2. 【メニュー戦略】人気メニューとセット内ドリンクの傾向・改善提案
3. 【集客・時間帯対策】ピーク時間の活用・閑散時間の改善策
4. 【来週の具体的アクション】3つの実行項目

結論は明確かつ実践的に、店主が明日から実行できるレベルで書いてください。`;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({
        model:'claude-sonnet-4-6',
        max_tokens:1000,
        messages:[{role:'user',content:prompt}]
      })
    });
    const data=await res.json();
    const text=data.content&&data.content[0]?data.content[0].text:'分析結果を取得できませんでした';
    document.getElementById('ai-result-area').innerHTML=`<div class="ai-result-box">${escHtml(text)}</div>`;
  }catch(e){
    document.getElementById('ai-result-area').innerHTML=`<div class="ai-result-box" style="color:var(--red);">通信エラーが発生しました。ネット接続を確認してください。\n\n${e.message}</div>`;
  }
  btn.disabled=false;
  btn.textContent='✨ AI で売上向上策を提案する';
}

function escHtml(s){ return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

/* ============================================================
   削除確認モーダル（閉じる）
   ============================================================ */
document.getElementById('confirm-modal-bg').addEventListener('click',function(e){
  if(e.target===this) closeConfirmModal();
});
document.getElementById('task-modal-bg').addEventListener('click',function(e){
  if(e.target===this) closeTaskModal();
});
document.getElementById('checkout-modal-bg').addEventListener('click',function(e){
  if(e.target===this) closeCheckoutModal();
});
document.getElementById('drink-select-modal-bg').addEventListener('click',function(e){
  if(e.target===this) closeDrinkSelectModal();
});
document.getElementById('dayclose-modal-bg').addEventListener('click',function(e){
  if(e.target===this) closeDayCloseModal();
});

/* ============================================================
   起動
   ============================================================ */
init();
</script>
</body>
</html>
