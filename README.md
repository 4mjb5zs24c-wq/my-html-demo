[tianxue-assistant-demo.html](https://github.com/user-attachments/files/28146394/tianxue-assistant-demo.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>天学网教师端</title>
<style>
:root{
  --primary:#4A90D9;--primary-dark:#3A7BC8;--primary-light:#E8F1FB;
  --bg:#F2F4F7;--white:#FFF;--text:#303133;--text-secondary:#606266;--text-muted:#909399;
  --border:#E4E7ED;--border-light:#EBEEF5;
  --shadow-sm:0 1px 3px rgba(0,0,0,.05);--shadow:0 2px 8px rgba(0,0,0,.07);
  --radius-sm:4px;--radius:8px;--radius-lg:12px;
  --font:-apple-system,BlinkMacSystemFont,"Segoe UI","PingFang SC","Microsoft YaHei","Helvetica Neue",sans-serif;
  --green:#26B979;--orange:#E6832A;--purple:#7C6FAD;--teal:#14B8A6;--pink:#EC4899;--red:#F56C6C;
  --sidebar-w:148px;--right-w:344px;--topbar-h:44px;--bottombar-h:36px;
  --card-purple-bg:#F3EEFC;--card-blue-bg:#EBF4FD;--card-yellow-bg:#FFF9ED;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:var(--font);background:var(--bg);color:var(--text);line-height:1.5;font-size:13px;-webkit-font-smoothing:antialiased;overflow:hidden;height:100vh;display:flex;flex-direction:column;}

/* ============================================================
   顶部导航栏
   ============================================================ */
.top-bar{height:var(--topbar-h);background:var(--white);display:flex;align-items:center;justify-content:space-between;padding:0 12px;border-bottom:1px solid var(--border-light);flex-shrink:0;}
.tb-center{display:flex;align-items:center;gap:16px;font-size:12px;color:var(--text-secondary);}
.tb-center .ver{color:var(--text-muted);}
.tb-center .book-select{display:flex;align-items:center;gap:4px;cursor:pointer;padding:3px 10px;border-radius:4px;background:#F5F7FA;font-size:12px;}
.tb-center .class-select{display:flex;align-items:center;gap:4px;cursor:pointer;padding:3px 10px;border-radius:4px;background:#F5F7FA;font-size:12px;}
.tb-right{display:flex;align-items:center;gap:10px;}
.tb-right .tb-icon{width:28px;height:28px;display:flex;align-items:center;justify-content:center;border-radius:4px;cursor:pointer;color:var(--text-secondary);font-size:14px;transition:all .15s;}
.tb-right .tb-icon:hover{background:#F0F2F5;}
.tb-right .btn-app{font-size:11px;padding:4px 10px;border-radius:4px;border:1px solid var(--border);background:#fff;cursor:pointer;color:var(--text-secondary);display:flex;align-items:center;gap:4px;}
.tb-right .btn-app:hover{background:#F5F7FA;}
.win-ctrl{display:flex;gap:2px;}
.win-ctrl .wc{width:28px;height:28px;display:flex;align-items:center;justify-content:center;border-radius:4px;cursor:pointer;color:var(--text-muted);font-size:12px;}
.win-ctrl .wc:hover{background:#F0F2F5;}
.win-ctrl .wc.close:hover{background:var(--red);color:#fff;}

/* ============================================================
   主体三栏布局
   ============================================================ */
.main-layout{display:flex;flex:1;overflow:hidden;}

/* ---- 左侧边栏 ---- */
.sidebar{width:var(--sidebar-w);background:var(--white);border-right:1px solid var(--border-light);display:flex;flex-direction:column;flex-shrink:0;overflow-y:auto;}
.sb-profile{display:flex;align-items:center;gap:8px;padding:14px 12px;border-bottom:1px solid var(--border-light);}
.sb-avatar{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,#4A90D9,#6DB3F2);display:flex;align-items:center;justify-content:center;color:#fff;font-size:16px;font-weight:600;flex-shrink:0;}
.sb-info{min-width:0;}
.sb-name{font-size:13px;font-weight:600;}
.sb-role{font-size:10px;color:var(--text-muted);}
.sb-nav{flex:1;padding:6px 0;display:flex;flex-direction:column;gap:2px;}
.sb-nav-item{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;padding:10px 8px;cursor:pointer;font-size:11px;color:var(--text-secondary);transition:all .15s;border-left:3px solid transparent;text-align:center;}
.sb-nav-item:hover{background:#F5F7FA;}
.sb-nav-item.active{background:var(--primary-light);color:var(--primary);border-left-color:var(--primary);font-weight:500;}
.sb-nav-item .sb-icon{font-size:18px;}

/* ---- 中间主内容 ---- */
.content-main{flex:1;overflow-y:auto;padding:16px 20px;display:flex;flex-direction:column;gap:16px;min-width:0;}

/* 模块区块 */
.module-section{background:var(--white);border-radius:var(--radius);padding:16px 20px;box-shadow:var(--shadow-sm);}
.module-section.fill{flex:1;display:flex;flex-direction:column;overflow:hidden;}
.module-section.fill .more-books{display:flex;flex-direction:column;}
.ms-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;}
.ms-title{font-size:15px;font-weight:600;display:flex;align-items:center;gap:8px;}
.ms-title::before{content:'';width:3px;height:14px;background:var(--primary);border-radius:2px;}

/* 布置练习 - 功能按钮行 */
.func-rows{display:flex;flex-direction:column;gap:10px;}
.func-row{display:flex;gap:10px;}
.func-btn{flex:1;display:flex;align-items:center;justify-content:center;padding:10px 0;border-radius:6px;font-size:12px;cursor:pointer;background:#F8FAFC;border:1px solid var(--border-light);color:var(--text-secondary);transition:all .15s;white-space:nowrap;}
.func-btn:hover{background:var(--primary-light);color:var(--primary);border-color:var(--primary-border);}

/* 智能搜索入口 */
.smart-search{display:flex;align-items:center;gap:10px;background:#F8FAFC;border-radius:20px;padding:8px 18px;cursor:pointer;font-size:12px;color:var(--text-muted);border:1px solid var(--border-light);transition:all .2s;min-width:280px;}
.smart-search:hover{border-color:var(--primary);background:#fff;}
.smart-search .ss-icon{font-size:15px;color:var(--primary);}
.smart-search .ss-text{color:var(--text-muted);}
.smart-search .ss-hint{font-size:11px;color:var(--primary);margin-left:auto;white-space:nowrap;}

/* 课堂教学 - 4个功能卡片 */
.teach-cards{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:16px;flex:1;}
.teach-card{border-radius:var(--radius);padding:18px 16px;cursor:pointer;transition:all .2s;position:relative;display:flex;flex-direction:column;justify-content:space-between;}
.teach-card:hover{transform:translateY(-2px);box-shadow:var(--shadow);}
.tc-purple{background:#F3EEFC;}
.tc-blue{background:#EBF4FD;}
.tc-yellow{background:#FFF9ED;}
.teach-card .tc-top{display:flex;flex-direction:column;}
.teach-card .tc-name{font-size:18px;font-weight:600;margin-bottom:4px;color:var(--text);}
.teach-card .tc-desc{font-size:11px;color:var(--text-muted);line-height:1.4;}
.teach-card .tc-icon{font-size:44px;align-self:flex-end;margin-top:auto;}
.teach-card .tc-badge{position:absolute;top:12px;right:14px;font-size:10px;padding:2px 8px;border-radius:8px;background:rgba(255,255,255,.8);font-weight:600;}

/* 更多课本 - 横向滚动 */
.more-books{margin-top:2px;}
.more-books .mb-title{font-size:13px;font-weight:600;margin-bottom:8px;display:flex;align-items:center;justify-content:space-between;}
.mb-scroll{display:flex;gap:10px;overflow-x:auto;padding-bottom:4px;}
.mb-scroll::-webkit-scrollbar{height:3px;}
.mb-scroll::-webkit-scrollbar-thumb{background:#ddd;border-radius:2px;}
.book-card{min-width:185px;background:#FAFBFC;border:1px solid var(--border-light);border-radius:var(--radius);padding:12px;cursor:pointer;transition:all .2s;flex-shrink:0;}
.book-card:hover{border-color:var(--primary-border);box-shadow:var(--shadow-sm);}
.book-card .bc-title{font-size:12px;font-weight:600;margin-bottom:3px;}
.book-card .bc-desc{font-size:10px;color:var(--text-muted);margin-bottom:8px;}
.book-card .bc-actions{display:flex;gap:6px;}
.book-card .bc-actions button{padding:4px 12px;border-radius:12px;font-size:11px;cursor:pointer;font-family:var(--font);transition:all .15s;}
.btn-outline{border:1px solid var(--primary);color:var(--primary);background:#fff;}
.btn-outline:hover{background:var(--primary-light);}
.btn-primary-sm{background:var(--primary);color:#fff;border:none;}
.btn-primary-sm:hover{background:var(--primary-dark);}

/* ---- 右侧面板 ---- */
.panel-right{width:var(--right-w);background:var(--bg);display:flex;flex-direction:column;flex-shrink:0;overflow-y:auto;}

/* 小天智能助手入口 */
.ai-entry-card{background:var(--white);margin:12px 12px 0 12px;padding:14px 16px;border-radius:var(--radius);border:1px solid var(--border-light);box-shadow:var(--shadow-sm);cursor:pointer;transition:all .2s;display:flex;align-items:center;justify-content:space-between;}
.ai-entry-card:hover{border-color:var(--primary);box-shadow:0 2px 8px rgba(74,144,217,.12);}
.ai-entry-left{display:flex;align-items:center;gap:10px;}
.ai-entry-left .aie-icon{width:38px;height:38px;border-radius:50%;background:linear-gradient(135deg,#4A90D9,#6DB3F2);display:flex;align-items:center;justify-content:center;font-size:18px;color:#fff;animation:aiPulse 2s infinite;}
@keyframes aiPulse{0%,100%{box-shadow:0 0 0 0 rgba(74,144,217,.4)}50%{box-shadow:0 0 0 10px rgba(74,144,217,.1)}}
.ai-entry-left .aie-text{font-size:13px;font-weight:600;}
.ai-entry-left .aie-sub{font-size:10px;color:var(--text-muted);}
.ai-entry-right{font-size:16px;color:var(--primary);transition:transform .3s;}
.ai-entry-right.expanded{transform:rotate(180deg);}

/* 练习报告 — 独立白色卡片 */
.report-section{margin:12px;padding:14px 16px;flex:1;overflow-y:auto;background:var(--white);border-radius:var(--radius);border:1px solid var(--border-light);box-shadow:var(--shadow-sm);}
.report-section::-webkit-scrollbar{width:3px;}
.report-section::-webkit-scrollbar-thumb{background:#ddd;border-radius:2px;}
.rs-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;}
.rs-title{font-size:14px;font-weight:600;}
.rs-filter{display:flex;align-items:center;gap:6px;}
.rs-filter select{font-size:11px;padding:3px 8px;border-radius:4px;border:1px solid var(--border);background:#fff;cursor:pointer;}
.rs-link{font-size:11px;color:var(--primary);cursor:pointer;text-decoration:none;}

.report-list{display:flex;flex-direction:column;gap:8px;}
.report-item{background:#FAFBFC;border:1px solid var(--border-light);border-radius:var(--radius);padding:12px;transition:all .15s;}
.report-item:hover{border-color:var(--primary-border);}
.report-item .ri-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;white-space:nowrap;}
.report-item .ri-name{font-size:13px;font-weight:600;overflow:hidden;text-overflow:ellipsis;}
.report-item .ri-class{font-size:11px;color:var(--text-muted);flex-shrink:0;margin-left:8px;}
.report-item .ri-bottom{display:flex;justify-content:space-between;align-items:center;white-space:nowrap;margin-top:6px;}
.ri-bottom .ri-time{font-size:10px;color:var(--text-muted);flex-shrink:0;margin-right:4px;}
.ri-bottom .ri-actions{display:flex;gap:3px;flex-shrink:0;white-space:nowrap;}
.ri-bottom .ri-actions button{padding:2px 7px;border-radius:8px;font-size:10px;cursor:pointer;font-family:var(--font);transition:all .15s;white-space:nowrap;flex-shrink:0;}

/* ============================================================
   底部控制栏
   ============================================================ */
.bottom-bar{height:var(--bottombar-h);background:var(--white);border-top:1px solid var(--border-light);display:flex;align-items:center;justify-content:space-between;padding:0 12px;flex-shrink:0;font-size:11px;color:var(--text-muted);}
.bb-left{display:flex;align-items:center;gap:8px;}
.bb-center{display:flex;align-items:center;gap:4px;cursor:pointer;padding:2px 10px;border-radius:4px;background:#F5F7FA;font-size:11px;}
.bb-right{display:flex;align-items:center;gap:8px;}
.bb-icon{width:24px;height:24px;display:flex;align-items:center;justify-content:center;border-radius:3px;cursor:pointer;font-size:12px;transition:all .15s;color:var(--text-muted);}
.bb-icon:hover{background:#F0F2F5;color:var(--text);}

/* ============================================================
   半屏AI助手浮窗
   ============================================================ */
.chat-overlay{position:fixed;inset:0;z-index:300;background:rgba(0,0,0,0.3);display:flex;align-items:stretch;justify-content:flex-end;opacity:0;pointer-events:none;transition:opacity .25s;}
.chat-overlay.open{opacity:1;pointer-events:auto;}
.chat-panel{width:50vw;min-width:560px;height:100vh;background:rgba(255,255,255,.98);backdrop-filter:blur(16px);box-shadow:-8px 0 40px rgba(0,0,0,.18);display:flex;flex-direction:column;overflow:hidden;transform:translateX(40px);transition:transform .3s ease;}
.chat-overlay.open .chat-panel{transform:translateX(0);}
.chat-header{background:linear-gradient(135deg,#4A90D9,#5FA3E8);color:#fff;padding:12px 16px;display:flex;align-items:center;justify-content:space-between;flex-shrink:0;}
.chat-hd-left{display:flex;align-items:center;gap:10px;}
.chat-hd-left .ch-icon{width:32px;height:32px;background:rgba(255,255,255,.22);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:16px;}
.chat-hd-left .ch-title{font-size:14px;font-weight:600;}
.chat-hd-left .ch-sub{font-size:10px;opacity:.85;}
.chat-hd-actions{display:flex;align-items:center;gap:6px;}
.chat-hd-btn{background:rgba(255,255,255,.15);border:none;color:#fff;height:28px;padding:0 10px;border-radius:14px;cursor:pointer;font-size:11px;font-family:var(--font);transition:all .2s;white-space:nowrap;display:flex;align-items:center;gap:3px;}
.chat-hd-btn:hover{background:rgba(255,255,255,.28);}
.chat-hd-btn.icon-only{width:28px;padding:0;justify-content:center;font-size:15px;}
.chat-close{background:rgba(255,255,255,.18);border:none;color:#fff;width:28px;height:28px;border-radius:50%;cursor:pointer;font-size:15px;display:flex;align-items:center;justify-content:center;transition:background .2s;flex-shrink:0;}
.chat-close:hover{background:rgba(255,255,255,.3);}
.chat-body{flex:1;overflow-y:auto;padding:14px 18px;display:flex;flex-direction:column;gap:10px;}
.chat-body::-webkit-scrollbar{width:4px;}
.chat-body::-webkit-scrollbar-thumb{background:#ddd;border-radius:2px;}

/* 消息气泡 */
.msg{display:flex;gap:7px;max-width:90%;animation:msgIn .25s ease;}
@keyframes msgIn{from{opacity:0;transform:translateY(4px)}to{opacity:1;transform:translateY(0)}}
.msg.assistant{align-self:flex-start;}
.msg.user{align-self:flex-end;flex-direction:row-reverse;}
.msg .avatar{width:28px;height:28px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:13px;}
.msg.assistant .avatar{background:var(--primary-light);color:var(--primary);}
.msg.user .avatar{background:#E9ECF1;color:var(--text-secondary);}
.msg .bubble{padding:8px 12px;border-radius:12px;font-size:12px;line-height:1.6;}
.msg.assistant .bubble{background:#F0F6FC;color:var(--text);border-top-left-radius:4px;}
.msg.user .bubble{background:#E9ECF1;color:var(--text);border-top-right-radius:4px;}
.msg.resource-push .bubble{background:#F5FAF7;border-left:3px solid var(--green);border-radius:6px 12px 12px 6px;}
.msg.workflow-guide .bubble{background:#FEF9F3;border-left:3px solid var(--orange);border-radius:6px 12px 12px 6px;}
.msg.guide-msg{max-width:100%;}
.msg.guide-msg .bubble{background:transparent;padding:0;}
.msg.guide-msg .avatar{display:none;}

/* 聊天卡片 */
.chat-cards{display:flex;flex-direction:column;gap:5px;margin-top:6px;}
.chat-card{background:#fff;border:1px solid var(--border-light);border-radius:6px;padding:9px 11px;cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:8px;}
.chat-card:hover{border-color:var(--primary);box-shadow:0 2px 6px rgba(74,144,217,.1);}
.chat-card .cc-icon{width:30px;height:30px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0;}
.chat-card .cc-info{flex:1;min-width:0;}
.chat-card .cc-name{font-size:12px;font-weight:600;}
.chat-card .cc-desc{font-size:10px;color:var(--text-muted);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.chat-card .cc-btn{font-size:10px;color:var(--primary);white-space:nowrap;padding:3px 8px;background:var(--primary-light);border-radius:8px;font-weight:500;}

/* 引导卡片 */
.guide-wrap{width:100%;}
.guide-title{text-align:center;font-size:17px;font-weight:600;color:var(--text);margin-bottom:4px;}
.guide-sub{text-align:center;font-size:11px;color:var(--text-muted);margin-bottom:12px;}
.guide-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;}
.guide-card{background:#fff;border:1px solid var(--border-light);border-radius:8px;padding:10px 12px;cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:8px;font-size:11px;color:var(--text-secondary);line-height:1.4;user-select:none;}
.guide-card:hover{background:#F5F9FD;border-color:var(--primary);color:var(--primary);box-shadow:0 2px 8px rgba(74,144,217,.1);transform:translateY(-1px);}
.guide-card .gc-icon{font-size:18px;flex-shrink:0;width:24px;text-align:center;}
.guide-card .gc-text{flex:1;min-width:0;}

/* 公共组件 */
.practice-options{display:flex;flex-wrap:wrap;gap:5px;margin-top:6px;}
.practice-opt{display:flex;align-items:center;gap:3px;padding:4px 8px;border-radius:12px;font-size:10px;cursor:pointer;background:#fff;border:1px solid var(--border);transition:all .15s;}
.practice-opt.selected,.practice-opt:hover{border-color:var(--primary);background:var(--primary);color:#fff;}
.word-chips{display:flex;flex-wrap:wrap;gap:5px;margin:6px 0;}
.word-chip{padding:3px 8px;border-radius:10px;font-size:11px;background:#fff;border:1px solid #DCE8F5;font-family:"SF Mono",Consolas,monospace;cursor:pointer;transition:all .15s;user-select:none;}
.word-chip.selected{background:var(--primary);color:#fff;border-color:var(--primary);}
.dictation-card,.assign-form{background:#fff;border:1px solid var(--border);border-radius:var(--radius);padding:12px;margin-top:6px;max-height:300px;overflow-y:auto;}
.dictation-card .dc-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;padding-bottom:8px;border-bottom:1px solid var(--border-light);}
.dictation-card .dc-table{width:100%;border-collapse:collapse;}
.dictation-card .dc-table th{background:#F8FAFC;padding:6px 8px;font-size:10px;color:var(--text-muted);text-align:left;font-weight:500;border-bottom:1px solid var(--border-light);}
.dictation-card .dc-table td{padding:6px 8px;font-size:11px;border-bottom:1px solid var(--border-light);}
.dictation-card .dc-table .dc-input{width:100%;border:1px dashed #ccc;border-radius:3px;padding:3px 5px;font-size:11px;font-family:var(--font);background:#FAFBFC;}
.dc-actions{margin-top:10px;display:flex;gap:6px;justify-content:flex-end;}
.dc-actions button,.dc-actions button.primary{padding:5px 12px;border-radius:12px;font-size:11px;cursor:pointer;font-family:var(--font);transition:all .15s;border:1px solid var(--border);background:#fff;color:var(--text-secondary);}
.dc-actions button.primary{background:var(--primary);color:#fff;border-color:var(--primary);}
.af-section{margin-bottom:8px;}
.af-section .afs-label{font-size:11px;font-weight:600;color:var(--text);margin-bottom:4px;}
.af-input{width:100%;border:1px solid var(--border);border-radius:4px;padding:6px 8px;font-size:11px;font-family:var(--font);outline:none;}
.af-input:focus{border-color:var(--primary);}
.pill-row,.check-row{display:flex;flex-wrap:wrap;gap:5px;}
.pill{display:flex;align-items:center;gap:3px;padding:4px 10px;border-radius:12px;font-size:10px;cursor:pointer;border:1px solid var(--border);background:#fff;transition:all .15s;font-family:var(--font);user-select:none;}
.pill.sel,.pill:hover{border-color:var(--primary);background:var(--primary);color:#fff;}
.check-item{display:flex;align-items:center;gap:4px;font-size:11px;cursor:pointer;padding:3px 6px;border-radius:4px;transition:all .15s;user-select:none;}
.check-item .ci-box{width:14px;height:14px;border:2px solid #C0C4CC;border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:9px;color:#fff;transition:all .15s;flex-shrink:0;}
.check-item .ci-box.checked{background:var(--primary);border-color:var(--primary);}
.toggle-wrap{display:flex;align-items:center;gap:6px;}
.toggle-sw{width:36px;height:20px;background:#C0C4CC;border-radius:10px;cursor:pointer;position:relative;transition:background .3s;}
.toggle-sw.on{background:var(--primary);}
.toggle-sw::after{content:'';position:absolute;top:2px;left:2px;width:16px;height:16px;background:#fff;border-radius:50%;transition:left .3s;box-shadow:0 1px 3px rgba(0,0,0,.2);}
.toggle-sw.on::after{left:18px;}
.toggle-label{font-size:11px;color:var(--text-secondary);}
.af-actions{display:flex;gap:6px;justify-content:flex-end;margin-top:6px;padding-top:6px;border-top:1px solid var(--border-light);}
.af-actions button{padding:6px 16px;border-radius:14px;font-size:11px;cursor:pointer;font-family:var(--font);border:none;transition:all .15s;}
.af-btn-cancel{background:#F2F3F5;color:var(--text-secondary);}
.af-btn-confirm{background:var(--primary);color:#fff;}
.success-card{background:linear-gradient(135deg,#EDF8F1,#F5FAF7);border:1px solid #B7E4CF;border-radius:var(--radius);padding:12px;margin-top:6px;text-align:center;}
.success-card .sc-check{font-size:28px;margin-bottom:4px;}
.success-card .sc-msg{font-size:13px;font-weight:600;color:var(--green);}
.success-card .sc-detail{font-size:10px;color:var(--text-muted);line-height:1.5;}
.completion-alert{background:#FFF8F0;border:1px solid #FDE2C3;border-radius:var(--radius);padding:10px;margin-top:6px;}
.completion-alert .ca-title{font-size:11px;font-weight:600;color:#B85C00;}
.completion-alert .ca-detail{font-size:10px;color:var(--text-secondary);margin:4px 0;}
.completion-alert .ca-actions{display:flex;gap:5px;}
.completion-alert .ca-actions button{padding:3px 10px;border-radius:10px;font-size:10px;cursor:pointer;font-family:var(--font);border:1px solid #FDE2C3;background:#fff;color:#B85C00;}
.stats-push{background:#fff;border:1px solid var(--border-light);border-radius:var(--radius);padding:10px;margin-top:6px;}
.stats-push .sp-title{font-size:12px;font-weight:600;margin-bottom:6px;}
.stats-push .sp-row{display:flex;justify-content:space-between;padding:3px 0;font-size:11px;color:var(--text-secondary);border-bottom:1px solid #F5F5F5;}
.stats-push .sp-row:last-child{border-bottom:none;}
.sp-val{font-weight:600;color:var(--text);}
.sp-val.warn{color:var(--orange);}

/* 历史下拉 */
.history-dropdown{position:absolute;top:40px;right:80px;background:#fff;border-radius:8px;box-shadow:0 8px 24px rgba(0,0,0,.15);width:240px;max-height:260px;overflow-y:auto;z-index:10;display:none;}
.history-dropdown.show{display:block;}
.history-dropdown .hd-item{padding:10px 14px;font-size:12px;color:var(--text);cursor:pointer;border-bottom:1px solid var(--border-light);transition:background .15s;}
.history-dropdown .hd-item:hover{background:#F5F7FA;}
.history-dropdown .hd-empty{padding:16px;text-align:center;font-size:12px;color:var(--text-muted);}

/* 全屏领读 */
.reading-overlay{position:fixed;inset:0;z-index:500;background:#1a1a2e;display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .3s;}
.reading-overlay.open{opacity:1;pointer-events:auto;}
.reading-page{width:100%;height:100%;display:flex;flex-direction:column;color:#fff;}
.reading-topbar{display:flex;align-items:center;justify-content:space-between;padding:14px 24px;background:rgba(255,255,255,.05);}
.reading-topbar .rt-title{font-size:18px;font-weight:600;}
.reading-topbar .rt-actions{display:flex;gap:10px;}
.reading-topbar button{padding:8px 18px;border-radius:16px;font-size:13px;cursor:pointer;font-family:var(--font);border:1px solid rgba(255,255,255,.3);background:rgba(255,255,255,.1);color:#fff;transition:all .2s;}
.reading-topbar button.primary{background:#4A90D9;border-color:#4A90D9;}
.reading-content{flex:1;display:flex;align-items:center;justify-content:center;padding:40px 80px;overflow-y:auto;}
.reading-content .rc-text{font-size:30px;line-height:2.2;text-align:center;max-width:900px;font-family:Georgia,"Times New Roman",serif;}
.reading-content .rc-vocab{display:flex;flex-wrap:wrap;gap:14px;justify-content:center;max-width:900px;}
.reading-content .rc-vocab .rv-word{text-align:center;padding:14px 22px;background:rgba(255,255,255,.08);border-radius:10px;min-width:110px;}
.reading-content .rc-vocab .rv-english{font-size:26px;font-weight:600;color:#FFD700;font-family:Georgia,serif;}
.reading-content .rc-vocab .rv-chinese{font-size:15px;color:rgba(255,255,255,.7);margin-top:4px;}
.reading-bottombar{display:flex;align-items:center;justify-content:center;gap:16px;padding:16px 24px;background:rgba(255,255,255,.05);}
.reading-bottombar button{width:44px;height:44px;border-radius:50%;border:2px solid rgba(255,255,255,.3);background:rgba(255,255,255,.1);color:#fff;font-size:18px;cursor:pointer;}
.reading-bottombar button.play-btn{width:56px;height:56px;background:#4A90D9;border-color:#4A90D9;font-size:22px;}
.reading-bottombar .rb-progress{font-size:13px;color:rgba(255,255,255,.6);}

/* 领读弹窗 */
.reading-modal-overlay{position:fixed;inset:0;z-index:450;background:rgba(0,0,0,.45);display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .25s;}
.reading-modal-overlay.open{opacity:1;pointer-events:auto;}
.reading-modal{background:#fff;border-radius:var(--radius-lg);padding:20px;width:380px;text-align:center;box-shadow:0 12px 40px rgba(0,0,0,.2);}
.reading-modal .rm-title{font-size:15px;font-weight:600;margin-bottom:6px;}
.reading-modal .rm-desc{font-size:12px;color:var(--text-muted);margin-bottom:14px;}
.reading-modal .rm-actions{display:flex;gap:8px;justify-content:center;}
.reading-modal .rm-actions button{padding:7px 18px;border-radius:14px;font-size:12px;cursor:pointer;font-family:var(--font);border:none;transition:all .15s;}
.rm-btn-secondary{background:#F2F3F5;color:var(--text-secondary);}
.rm-btn-primary{background:var(--primary);color:#fff;}

/* 快捷提问 & 输入 */
.quick-chips{display:flex;flex-wrap:wrap;gap:5px;padding:6px 16px 14px;flex-shrink:0;}
.quick-chip{background:#F0F6FC;color:var(--primary);border:1px solid #D0E2F7;border-radius:12px;padding:3px 10px;font-size:10px;cursor:pointer;transition:all .2s;white-space:nowrap;font-family:var(--font);}
.quick-chip:hover{background:var(--primary);color:#fff;border-color:var(--primary);}
.chat-input-wrap{padding:10px 16px 14px;border-top:1px solid var(--border-light);display:flex;gap:6px;flex-shrink:0;}
.chat-input-wrap input{flex:1;border:1px solid var(--border);border-radius:16px;padding:8px 12px;font-size:12px;outline:none;font-family:var(--font);transition:border-color .2s;}
.chat-input-wrap input:focus{border-color:var(--primary);}
.chat-input-wrap button{background:var(--primary);color:#fff;border:none;border-radius:16px;padding:8px 16px;cursor:pointer;font-size:12px;font-weight:500;transition:background .2s;font-family:var(--font);}
.chat-input-wrap button:hover{background:var(--primary-dark);}
.chat-input-wrap button:disabled{background:#C0C4CC;cursor:not-allowed;}

.toast{position:fixed;top:20px;left:50%;transform:translateX(-50%);background:#303133;color:#fff;padding:10px 24px;border-radius:20px;font-size:13px;z-index:999;opacity:0;transition:opacity .3s;pointer-events:none;}
.toast.show{opacity:1;}
.typing-dots{display:flex;gap:3px;padding:2px 0;}
.typing-dots span{width:5px;height:5px;background:#90B8E0;border-radius:50%;animation:tb 1.2s infinite;}
.typing-dots span:nth-child(2){animation-delay:.2s;}
.typing-dots span:nth-child(3){animation-delay:.4s;}
@keyframes tb{0%,60%,100%{transform:translateY(0);opacity:.4}30%{transform:translateY(-5px);opacity:1}}

/* ============================================================
   展开式资源卡片 (聊天内)
   ============================================================ */
.expand-card{background:#fff;border:1px solid var(--border-light);border-radius:var(--radius);overflow:hidden;margin-top:6px;transition:all .2s;}
.expand-card .ec-header{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;cursor:pointer;transition:background .15s;}
.expand-card .ec-header:hover{background:#F8FAFC;}
.expand-card .ec-hd-left{display:flex;align-items:center;gap:10px;}
.expand-card .ec-hd-icon{font-size:20px;width:32px;height:32px;border-radius:8px;display:flex;align-items:center;justify-content:center;}
.expand-card .ec-hd-name{font-size:13px;font-weight:600;}
.expand-card .ec-hd-count{font-size:11px;color:var(--text-muted);}
.expand-card .ec-arrow{font-size:12px;color:var(--text-muted);transition:transform .25s;}
.expand-card.open .ec-arrow{transform:rotate(180deg);}
.expand-card .ec-body{display:none;padding:0 14px 10px;}
.expand-card.open .ec-body{display:block;}
.expand-card .ec-item{display:flex;align-items:center;gap:8px;padding:6px 0;font-size:11px;color:var(--text-secondary);cursor:pointer;border-bottom:1px solid #F5F5F5;}
.expand-card .ec-item:last-child{border-bottom:none;}
.expand-card .ec-item .ec-check{width:15px;height:15px;border:2px solid #C0C4CC;border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:9px;color:#fff;transition:all .15s;flex-shrink:0;}
.expand-card .ec-item .ec-check.checked{background:var(--primary);border-color:var(--primary);}
.expand-card .ec-footer{display:none;padding:8px 14px;border-top:1px solid var(--border-light);gap:6px;}
.expand-card.open .ec-footer{display:flex;}
.expand-card .ec-footer button{padding:5px 14px;border-radius:14px;font-size:11px;cursor:pointer;font-family:var(--font);border:none;transition:all .15s;}

/* 练习选择弹窗 */
.practice-modal-overlay{position:fixed;inset:0;z-index:350;background:rgba(0,0,0,.35);display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .25s;}
.practice-modal-overlay.open{opacity:1;pointer-events:auto;}
.practice-modal{background:#fff;border-radius:var(--radius-lg);padding:24px;width:440px;max-height:560px;overflow-y:auto;box-shadow:0 16px 48px rgba(0,0,0,.18);}
.practice-modal .pm-title{font-size:16px;font-weight:600;margin-bottom:4px;}
.practice-modal .pm-sub{font-size:12px;color:var(--text-muted);margin-bottom:16px;}
.practice-modal .pm-list{display:flex;flex-direction:column;gap:6px;}
.practice-modal .pm-item{display:flex;align-items:center;gap:10px;padding:10px 12px;border:1px solid var(--border-light);border-radius:8px;cursor:pointer;transition:all .15s;}
.practice-modal .pm-item:hover{border-color:var(--primary);background:#F8FBFF;}
.practice-modal .pm-item.sel{border-color:var(--primary);background:var(--primary-light);}
.practice-modal .pm-item .pm-radio{width:18px;height:18px;border:2px solid #C0C4CC;border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all .15s;}
.practice-modal .pm-item.sel .pm-radio{border-color:var(--primary);}
.practice-modal .pm-item.sel .pm-radio::after{content:'';width:10px;height:10px;border-radius:50%;background:var(--primary);}
.practice-modal .pm-item .pm-info{flex:1;}
.practice-modal .pm-item .pm-name{font-size:13px;font-weight:600;}
.practice-modal .pm-item .pm-desc{font-size:10px;color:var(--text-muted);}
.practice-modal .pm-actions{display:flex;gap:8px;justify-content:flex-end;margin-top:16px;}
.practice-modal .pm-actions button{padding:7px 20px;border-radius:16px;font-size:12px;cursor:pointer;font-family:var(--font);border:none;transition:all .15s;}

/* 全屏听写 / 听力 / 视频页 */
.fullscreen-page{position:fixed;inset:0;z-index:500;background:#F2F4F7;display:flex;flex-direction:column;opacity:0;pointer-events:none;transition:opacity .3s;}
.fullscreen-page.open{opacity:1;pointer-events:auto;}
.fsp-topbar{display:flex;align-items:center;justify-content:space-between;padding:12px 20px;background:#fff;border-bottom:1px solid var(--border-light);}
.fsp-topbar .fsp-title{font-size:16px;font-weight:600;}
.fsp-topbar button{padding:6px 16px;border-radius:14px;font-size:12px;cursor:pointer;font-family:var(--font);border:1px solid var(--border);background:#fff;transition:all .15s;}
.fsp-topbar button:hover{background:#F5F7FA;}
.fsp-body{flex:1;display:flex;align-items:center;justify-content:center;padding:40px;overflow-y:auto;}
.fsp-body .fsp-content{max-width:700px;width:100%;text-align:center;}
.fsp-body .fsp-word{font-size:42px;font-weight:700;color:var(--text);margin-bottom:8px;font-family:Georgia,serif;}
.fsp-body .fsp-meaning{font-size:18px;color:var(--text-muted);margin-bottom:24px;}
.fsp-body .fsp-input{width:100%;max-width:400px;padding:12px 16px;font-size:18px;border:2px solid var(--border);border-radius:8px;text-align:center;outline:none;font-family:var(--font);}
.fsp-body .fsp-input:focus{border-color:var(--primary);}
.fsp-body .fsp-audio-icon{font-size:64px;margin-bottom:16px;cursor:pointer;}
.fsp-body .fsp-video-placeholder{width:100%;max-width:640px;height:360px;background:#1a1a2e;border-radius:12px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:48px;}
.fsp-bottombar{display:flex;align-items:center;justify-content:center;gap:12px;padding:14px 20px;background:#fff;border-top:1px solid var(--border-light);}
.fsp-bottombar button{padding:8px 24px;border-radius:16px;font-size:13px;cursor:pointer;font-family:var(--font);border:none;transition:all .15s;}
</style>
</head>
<body>

<!-- ============================================================
     顶部导航栏
     ============================================================ -->
<div class="top-bar">
  <div style="width:var(--sidebar-w);"></div>
  <div class="tb-center">
    <span class="ver">v 2.0.3</span>
    <span class="book-select">教材：仁爱版 ▾</span>
    <span class="class-select">初一1班 ▾</span>
  </div>
  <div class="tb-right">
    <span class="tb-icon" title="消息">🔔</span>
    <button class="btn-app">📱 下载APP</button>
    <span class="tb-icon" title="菜单">☰</span>
    <span class="win-ctrl">
      <span class="wc" title="最小化">─</span>
      <span class="wc" title="最大化">☐</span>
      <span class="wc close" title="关闭">✕</span>
    </span>
  </div>
</div>

<!-- ============================================================
     主体三栏布局
     ============================================================ -->
<div class="main-layout">

  <!-- 左侧边栏 -->
  <div class="sidebar">
    <div class="sb-profile">
      <div class="sb-avatar">牛</div>
      <div class="sb-info"><div class="sb-name">牛老师</div><div class="sb-role">英语 · 初一</div></div>
    </div>
    <div class="sb-nav">
      <div class="sb-nav-item active"><span class="sb-icon">🏠</span>首页</div>
      <div class="sb-nav-item"><span class="sb-icon">📄</span>我的备课</div>
      <div class="sb-nav-item"><span class="sb-icon">📝</span>智能阅卷</div>
      <div class="sb-nav-item"><span class="sb-icon">📓</span>错题本</div>
      <div class="sb-nav-item"><span class="sb-icon">📊</span>班级错题本</div>
      <div class="sb-nav-item"><span class="sb-icon">📚</span>学生个性化词本</div>
      <div class="sb-nav-item"><span class="sb-icon">⋯</span>更多功能</div>
    </div>
  </div>

  <!-- 中间主内容 -->
  <div class="content-main">

    <!-- 布置练习 -->
    <div class="module-section">
      <div class="ms-header"><span class="ms-title">布置练习</span></div>
      <div class="func-rows">
        <div class="func-row">
          <span class="func-btn">同步</span>
          <span class="func-btn">专项</span>
          <span class="func-btn">模拟</span>
          <span class="func-btn">趣味配音</span>
          <span class="func-btn">时文阅读</span>
        </div>
        <div class="func-row">
          <span class="func-btn">主题视频</span>
          <span class="func-btn">课后PK</span>
          <span class="func-btn">选题组卷</span>
          <span class="func-btn">试卷/答题卡</span>
          <span class="func-btn">自定义批改</span>
        </div>
      </div>
    </div>

    <!-- 课堂教学 -->
    <div class="module-section fill">
      <div class="ms-header">
        <span class="ms-title">课堂教学</span>
        <div class="smart-search" id="smartSearchEntry">
          <span class="ss-icon">🔍</span><span class="ss-text">智能搜索</span>
          <span class="ss-hint">快速找到想要的功能？点我试试~</span>
        </div>
      </div>
      <div class="teach-cards">
        <div class="teach-card tc-purple"><div class="tc-top"><div class="tc-name">同步教学</div><div class="tc-desc">同步课文·跟读·词汇</div></div><div class="tc-icon">📖</div></div>
        <div class="teach-card tc-purple"><div class="tc-top"><div class="tc-name">中考复习</div><div class="tc-desc">中考真题·模拟训练</div></div><div class="tc-icon">🎓</div></div>
        <div class="teach-card tc-blue"><div class="tc-top"><div class="tc-name">作文练习</div><div class="tc-desc">智能批改·范文推荐</div></div><div class="tc-icon">✍️</div><span class="tc-badge">AI</span></div>
        <div class="teach-card tc-yellow"><div class="tc-top"><div class="tc-name">词汇PK</div><div class="tc-desc">单词竞赛·班级PK</div></div><div class="tc-icon">⚡</div><span class="tc-badge">PK</span></div>
      </div>
      <div class="more-books">
        <div class="mb-title"><span>更多课本</span><span style="font-size:11px;color:var(--primary);cursor:pointer;">查看全部 ›</span></div>
        <div class="mb-scroll">
          <div class="book-card"><div class="bc-title">Unit 1 Making New Friends</div><div class="bc-desc">仁爱版 · 七年级上册</div><div class="bc-actions"><button class="btn-outline">布置</button><button class="btn-primary-sm">进入</button></div></div>
          <div class="book-card"><div class="bc-title">Unit 2 Looking Different</div><div class="bc-desc">仁爱版 · 七年级上册</div><div class="bc-actions"><button class="btn-outline">布置</button><button class="btn-primary-sm">进入</button></div></div>
          <div class="book-card"><div class="bc-title">Unit 3 Getting Together</div><div class="bc-desc">仁爱版 · 七年级上册</div><div class="bc-actions"><button class="btn-outline">布置</button><button class="btn-primary-sm">进入</button></div></div>
          <div class="book-card"><div class="bc-title">Unit 4 Having Fun</div><div class="bc-desc">仁爱版 · 七年级上册</div><div class="bc-actions"><button class="btn-outline">布置</button><button class="btn-primary-sm">进入</button></div></div>
          <div class="book-card"><div class="bc-title">Unit 5 Our School Life</div><div class="bc-desc">仁爱版 · 七年级上册</div><div class="bc-actions"><button class="btn-outline">布置</button><button class="btn-primary-sm">进入</button></div></div>
        </div>
      </div>
    </div>
  </div>

  <!-- 右侧面板 -->
  <div class="panel-right">

    <!-- 小天智能助手入口 -->
    <div class="ai-entry-card" id="aiEntryCard">
      <div class="ai-entry-left">
        <div class="aie-icon">✨</div>
        <div><div class="aie-text">小天智能助手</div><div class="aie-sub">点击展开 · 智能教学导航</div></div>
      </div>
      <span class="ai-entry-right" id="aiEntryArrow">▾</span>
    </div>

    <!-- 练习报告 -->
    <div class="report-section">
      <div class="rs-header">
        <span class="rs-title">练习报告</span>
        <div class="rs-filter">
          <select><option>全部</option><option>本周</option><option>本月</option></select>
          <a class="rs-link">查看全部列表 ›</a>
        </div>
      </div>
      <div class="report-list">
        <div class="report-item">
          <div class="ri-top"><span class="ri-name">Unit1 词汇听写练习</span><span class="ri-class">初一1班</span></div>
          <div class="ri-bottom"><span class="ri-time">05-14 布置 · 05-20 截止</span><div class="ri-actions"><button class="btn-outline" style="font-size:10px;">全屏讲解</button><button class="btn-primary-sm" style="font-size:10px;">报告</button></div></div>
        </div>
        <div class="report-item">
          <div class="ri-top"><span class="ri-name">Unit1 同步课文跟读</span><span class="ri-class">初一1班</span></div>
          <div class="ri-bottom"><span class="ri-time">05-10 布置 · 05-18 截止</span><div class="ri-actions"><button class="btn-outline" style="font-size:10px;">全屏讲解</button><button class="btn-primary-sm" style="font-size:10px;">报告</button></div></div>
        </div>
        <div class="report-item">
          <div class="ri-top"><span class="ri-name">Unit1 听说专项练习</span><span class="ri-class">初一3班</span></div>
          <div class="ri-bottom"><span class="ri-time">05-08 布置 · 05-22 截止</span><div class="ri-actions"><button class="btn-outline" style="font-size:10px;">全屏讲解</button><button class="btn-primary-sm" style="font-size:10px;">报告</button></div></div>
        </div>
        <div class="report-item">
          <div class="ri-top"><span class="ri-name">听说练习一</span><span class="ri-class">初一1班</span></div>
          <div class="ri-bottom"><span class="ri-time">05-12 布置 · 05-22 截止</span><div class="ri-actions"><button class="btn-outline" style="font-size:10px;">全屏讲解</button><button class="btn-primary-sm" style="font-size:10px;">报告</button></div></div>
        </div>
        <div class="report-item">
          <div class="ri-top"><span class="ri-name">听说练习二</span><span class="ri-class">初一2班</span></div>
          <div class="ri-bottom"><span class="ri-time">05-12 布置 · 05-22 截止</span><div class="ri-actions"><button class="btn-outline" style="font-size:10px;">全屏讲解</button><button class="btn-primary-sm" style="font-size:10px;">报告</button></div></div>
        </div>
        <div class="report-item">
          <div class="ri-top"><span class="ri-name">听说练习三</span><span class="ri-class">初一3班</span></div>
          <div class="ri-bottom"><span class="ri-time">05-12 布置 · 05-22 截止</span><div class="ri-actions"><button class="btn-outline" style="font-size:10px;">全屏讲解</button><button class="btn-primary-sm" style="font-size:10px;">报告</button></div></div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ============================================================
     底部控制栏
     ============================================================ -->
<div class="bottom-bar">
  <div class="bb-left">
    <span class="bb-icon">⏻</span>
    <span class="bb-icon">─</span>
  </div>
  <div class="bb-center">初一1班 ▾</div>
  <div class="bb-right">
    <span class="bb-icon">─</span>
    <span class="bb-icon">✕</span>
    <span class="bb-icon" id="bbAiToggle" title="小天智能助手">✨</span>
  </div>
</div>

<!-- ============================================================
     半屏AI助手浮窗
     ============================================================ -->
<div class="chat-overlay" id="chatOverlay">
  <div class="chat-panel">
    <div class="chat-header">
      <div class="chat-hd-left"><div class="ch-icon">✨</div><div><div class="ch-title">小天智能助手</div><div class="ch-sub">用自然语言告诉我你想做什么</div></div></div>
      <div class="chat-hd-actions">
        <button class="chat-hd-btn icon-only" id="btnNewChat" title="新建对话">＋</button>
        <button class="chat-hd-btn icon-only" id="btnHistory" title="对话历史">🕐</button>
        <button class="chat-close" id="chatClose">✕</button>
      </div>
      <div class="history-dropdown" id="historyDropdown"></div>
    </div>
    <div class="chat-body" id="chatMessages"></div>
    <div class="quick-chips" id="quickChips">
      <span class="quick-chip" data-query="推送U1单元的同步教学资源">推送U1资源</span>
      <span class="quick-chip" data-query="找Unit1的内容">找Unit1内容</span>
      <span class="quick-chip" data-query="帮我准备Unit2的练习">准备Unit2练习</span>
      <span class="quick-chip" data-query="good, morning, welcome">单词听写</span>
      <span class="quick-chip" data-query="给初一1班布置同步练习">布置练习</span>
      <span class="quick-chip" data-query="查看班级学情数据">查看学情</span>
      <span class="quick-chip" data-query="帮我推荐写作练习资源">写作练习</span>
      <span class="quick-chip" data-query="怎么进入错题本">错题本</span>
    </div>
    <div class="chat-input-wrap">
      <input type="text" id="chatInput" placeholder='输入你的问题，如"帮我找Unit1的词汇课件"…' maxlength="300">
      <button id="chatSend">发送</button>
    </div>
  </div>
</div>

<!-- 全屏领读 -->
<div class="reading-overlay" id="readingOverlay">
  <div class="reading-page">
    <div class="reading-topbar"><span class="rt-title" id="readingTitle">📖 课文领读</span><div class="rt-actions"><button onclick="window._tx_toggleReadingMode()" id="btnReadingMode">🔤 词汇模式</button><button class="primary" onclick="window._tx_closeReading()">✕ 退出领读</button></div></div>
    <div class="reading-content" id="readingContent"></div>
    <div class="reading-bottombar"><button onclick="window._tx_readingPrev()">⏮</button><button class="play-btn" onclick="window._tx_readingPlay()" id="btnPlay">▶</button><button onclick="window._tx_readingNext()">⏭</button><span class="rb-progress" id="readingProgress">1/1</span></div>
  </div>
</div>
<div class="reading-modal-overlay" id="readingModalOverlay">
  <div class="reading-modal"><div class="rm-title">📖 进入领读模式</div><div class="rm-desc" id="readingModalDesc">已选择 0 个单词</div><div class="rm-actions"><button class="rm-btn-secondary" onclick="window._tx_closeReadingModal()">取消</button><button class="rm-btn-primary" onclick="window._tx_startReading()">进入全屏领读</button></div></div>
</div>
<div class="toast" id="toast"></div>

<!-- 练习选择弹窗 -->
<div class="practice-modal-overlay" id="practiceModalOverlay">
  <div class="practice-modal">
    <div class="pm-title">选择要布置的练习</div>
    <div class="pm-sub" id="pmSub">请选择一项练习进行布置</div>
    <div class="pm-list" id="pmList"></div>
    <div class="pm-actions">
      <button class="af-btn-cancel" onclick="window._tx_closePracticeModal()">取消</button>
      <button class="af-btn-confirm" id="pmConfirm" onclick="window._tx_confirmPracticeSelect()">下一步：布置设置</button>
    </div>
  </div>
</div>

<!-- 全屏单词听写页 -->
<div class="fullscreen-page" id="dictationPage">
  <div class="fsp-topbar"><span class="fsp-title">📝 单词听写</span><button onclick="window._tx_closeFullscreen('dictationPage')">✕ 退出</button></div>
  <div class="fsp-body"><div class="fsp-content"><div class="fsp-word" id="dictWord">good</div><div class="fsp-meaning" id="dictMeaning">好的</div><input class="fsp-input" id="dictInput" placeholder="输入你听到的单词..." autocomplete="off"></div></div>
  <div class="fsp-bottombar"><button class="af-btn-cancel" onclick="window._tx_closeFullscreen('dictationPage')">结束听写</button><button class="af-btn-confirm" id="dictNext" onclick="window._tx_nextDictationWord()">下一个 ›</button></div>
</div>

<!-- 全屏听力练习页 -->
<div class="fullscreen-page" id="listeningPage">
  <div class="fsp-topbar"><span class="fsp-title">🎧 听力练习</span><button onclick="window._tx_closeFullscreen('listeningPage')">✕ 退出</button></div>
  <div class="fsp-body"><div class="fsp-content"><div class="fsp-audio-icon">🔊</div><div class="fsp-word">Unit 1 Listening Task</div><div class="fsp-meaning">点击播放按钮开始听力练习</div></div></div>
  <div class="fsp-bottombar"><button class="af-btn-cancel" onclick="window._tx_closeFullscreen('listeningPage')">退出</button><button class="af-btn-confirm" onclick="showToast('模拟播放中…（Demo）')">▶ 播放</button></div>
</div>

<!-- 全屏视频播放页 -->
<div class="fullscreen-page" id="videoPage">
  <div class="fsp-topbar"><span class="fsp-title" id="videoPageTitle">🎬 主题视频</span><button onclick="window._tx_closeFullscreen('videoPage')">✕ 退出</button></div>
  <div class="fsp-body"><div class="fsp-content"><div class="fsp-video-placeholder">▶</div><div class="fsp-meaning" style="margin-top:16px;" id="videoPageDesc">视频播放区域</div></div></div>
  <div class="fsp-bottombar"><button class="af-btn-cancel" onclick="window._tx_closeFullscreen('videoPage')">退出</button><button class="af-btn-confirm" onclick="showToast('模拟播放中…（Demo）')">▶ 播放</button></div>
</div>

<!-- ============================================================
     JavaScript
     ============================================================ -->
<script>
(function(){
'use strict';

const FUNCTION_DB=[
  {id:'sync-teach',name:'同步教学',desc:'教材同步课件、课文跟读、课堂互动',icon:'📖',iClass:'i-blue',keywords:['同步教学','课文','跟读']},
  {id:'special-practice',name:'专项练习',desc:'词汇、语法、听说、阅读专项训练',icon:'📝',iClass:'i-green',keywords:['专项练习','词汇','语法','听说','阅读']},
  {id:'mock-exam',name:'模拟考试',desc:'单元测试、期中期末模拟卷',icon:'📋',iClass:'i-orange',keywords:['模拟考试','考试','测试']},
  {id:'fun-dubbing',name:'趣味配音',desc:'课文配音、角色扮演',icon:'🎙️',iClass:'i-purple',keywords:['配音','角色扮演']},
  {id:'current-reading',name:'时文阅读',desc:'热点英文时文、分层阅读',icon:'📰',iClass:'i-teal',keywords:['时文','阅读']},
  {id:'theme-video',name:'主题视频',desc:'单元主题英文短视频',icon:'🎬',iClass:'i-pink',keywords:['视频','主题视频']},
  {id:'error-notebook',name:'错题本',desc:'个人和班级错题统计',icon:'📋',iClass:'i-orange',keywords:['错题','错题本']},
  {id:'practice-report',name:'练习报告',desc:'练习完成情况和成绩分析',icon:'📈',iClass:'i-blue',keywords:['报告','成绩','练习报告','学情']},
  {id:'smart-grading',name:'智能阅卷',desc:'辅助批改客观题和主观题',icon:'🤖',iClass:'i-purple',keywords:['阅卷','批改']},
  {id:'assign-practice',name:'布置练习',desc:'布置同步/专项/自定义练习',icon:'📝',iClass:'i-green',keywords:['布置','练习','作业']},
];
const RESOURCE_DB=[
  {id:'sync-text',name:'同步课文',desc:'逐句跟读、翻译和背诵',icon:'📖',iClass:'i-blue',keywords:['课文','跟读','逐句','背诵']},
  {id:'sync-vocab',name:'同步词汇',desc:'单词听写、词汇巩固练习',icon:'📚',iClass:'i-green',keywords:['词汇','单词','听写']},
  {id:'special-practice-res',name:'专项练习',desc:'听说、语法、阅读、写作',icon:'🎯',iClass:'i-orange',keywords:['专项','听说','语法']},
  {id:'fun-dubbing-res',name:'趣味配音',desc:'课文片段角色扮演',icon:'🎙️',iClass:'i-purple',keywords:['配音','角色扮演']},
  {id:'current-reading-res',name:'时文阅读',desc:'热点话题英文时文',icon:'🌍',iClass:'i-teal',keywords:['时文','阅读','热点']},
  {id:'theme-video-res',name:'主题视频',desc:'单元主题英文短视频',icon:'🎬',iClass:'i-pink',keywords:['视频','主题视频']},
  {id:'lecture-ppt',name:'讲评课件',desc:'自动生成讲评PPT',icon:'🖥️',iClass:'i-blue',keywords:['讲评','PPT','课件']},
  {id:'exam-papers',name:'试卷答题卡',desc:'单元测试卷和答题卡',icon:'📄',iClass:'i-orange',keywords:['试卷','答题卡']},
  {id:'listening',name:'听力材料',desc:'教材同步听力与训练',icon:'🎧',iClass:'i-green',keywords:['听力','音频','听说']},
  {id:'writing-correction',name:'作文批改',desc:'英语作文智能批改',icon:'✍️',iClass:'i-purple',keywords:['作文','写作','批改']},
];
const PRACTICE_FORMS=[
  {id:'sentence-read',name:'逐句跟读',icon:'🎤',desc:'逐句朗读，评测发音'},
  {id:'word-dictation',name:'单词听写',icon:'✏️',desc:'英文/中文/中英混合'},
  {id:'choice-exercise',name:'选择练习',icon:'🔤',desc:'单选、多选巩固知识'},
  {id:'fill-blank',name:'填空练习',icon:'📝',desc:'上下文填入正确单词'},
  {id:'role-play',name:'角色扮演',icon:'🎭',desc:'分角色朗读课文对话'},
];
const UNIT_CONTENT_DB={
  'unit1':{unitName:'Unit 1',fullName:'Making New Friends',book:'仁爱版七年级上册',textTitle:'Making New Friends',textFull:"Good morning! I'm Kangkang. I'm twelve years old. I'm a student in Class One, Grade Seven. I have a good friend. His name is Michael. He is from the USA. He is tall and he has big blue eyes. We are in the same class. Miss Wang is our English teacher. She is kind and helpful. We all like her very much.",vocab:['morning','welcome','China','thank','hello','friend','student','teacher','class','grade','twelve','year','old','from','USA','tall','blue','eye','same','kind','helpful','very','much'],vocabCN:{morning:'早晨',welcome:'欢迎',China:'中国',thank:'谢谢',hello:'你好',friend:'朋友',student:'学生',teacher:'老师',class:'班级',grade:'年级',twelve:'十二',year:'年',old:'老的',from:'来自',USA:'美国',tall:'高的',blue:'蓝色的',eye:'眼睛',same:'相同的',kind:'友善的',helpful:'有帮助的',very:'非常',much:'许多'},themeVideos:[{title:'《张雪机车中国骄傲》',desc:'励志主题',duration:'4:32'},{title:'《地球日环保行动》',desc:'常识主题',duration:'3:58'}],currentReadings:[{title:'《人工智能如何改变沟通方式》',desc:'科技·AI翻译',level:'中等',words:320},{title:'《可以"吃"电子垃圾的细菌》',desc:'科学·微生物',level:'中等',words:280}],resources:['sync-text','sync-vocab','listening','theme-video-res','current-reading-res'],practiceForms:['sentence-read','word-dictation','choice-exercise','fill-blank'],essay:{title:'My Best Friend',content:'A true friend is someone who always stands by your side. In my life, I am lucky to have such a friend. His name is Michael. We have known each other since primary school. Whenever I face difficulties, he is the first person to offer help. He never ignores my feelings and always shows great concern for me. I believe friendship is one of the most precious gifts in life.'}},
  'unit2':{unitName:'Unit 2',fullName:'Looking Different',book:'仁爱版七年级上册',textTitle:'Looking Different',textFull:"I have a sister. Her name is Maria. She is thirteen years old. She has long brown hair and big green eyes. She is not tall but she is very cute. We look different but we love each other very much. She likes singing and dancing. I like playing basketball. After school, we often do our homework together.",vocab:['sister','thirteen','long','brown','hair','green','cute','look','different','love','sing','dance','basketball','after','school','often','homework','together'],vocabCN:{sister:'姐妹',thirteen:'十三',long:'长的',brown:'棕色的',hair:'头发',green:'绿色的',cute:'可爱的',look:'看起来',different:'不同的',love:'爱',sing:'唱歌',dance:'跳舞',basketball:'篮球',after:'之后',school:'学校',often:'经常',homework:'作业',together:'一起'},themeVideos:[{title:'《世界各地的早餐文化》',desc:'文化主题',duration:'5:10'},{title:'《均衡膳食的科学》',desc:'科普主题',duration:'4:45'}],currentReadings:[{title:'《未来食物：昆虫蛋白》',desc:'科技·可持续',level:'中等',words:350},{title:'《改变全校饮食习惯的厨师》',desc:'人物·健康饮食',level:'简单',words:260}],resources:['sync-text','sync-vocab','listening','special-practice-res','lecture-ppt'],practiceForms:['sentence-read','word-dictation','choice-exercise','fill-blank','role-play'],essay:{title:'Healthy Eating Habits',content:'Healthy eating is not just about strict nutrition rules, but about maintaining a balanced diet. First, we should eat a variety of foods, including fresh vegetables, fruits, whole grains, and lean proteins. Second, it is important to control portion sizes. Third, we should not skip breakfast. Finally, we should reduce processed food. A healthy diet leads to a healthy body and a sharp mind.'}},
  'unit3':{unitName:'Unit 3',fullName:'Getting Together',book:'仁爱版七年级上册',textTitle:'Getting Together',textFull:"It is Sunday today. Kangkang and his friends are having a picnic in the park. Jane is singing an English song. Maria is playing the guitar. Michael is flying a kite. Kangkang is cooking some food. They are all very happy. Miss Wang is also there. She is helping them take photos. Everyone is having a great time together.",vocab:['Sunday','picnic','park','song','guitar','kite','cook','food','happy','photo','great','time','everyone','today','English','play','fly','help'],vocabCN:{Sunday:'星期天',picnic:'野餐',park:'公园',song:'歌曲',guitar:'吉他',kite:'风筝',cook:'烹饪',food:'食物',happy:'开心的',photo:'照片',great:'很棒的',time:'时间',everyone:'每个人',today:'今天',English:'英语',play:'玩',fly:'飞',help:'帮助'},themeVideos:[{title:'《马克·吐温的文学世界》',desc:'人文主题',duration:'6:20'},{title:'《伦敦百年变迁》',desc:'历史主题',duration:'5:05'}],currentReadings:[{title:'《如果钱不是问题》',desc:'思辨·金钱与幸福',level:'中等',words:300},{title:'《一枚硬币的环球旅行》',desc:'趣味·货币流通',level:'简单',words:240}],resources:['sync-text','sync-vocab','listening','fun-dubbing-res','current-reading-res'],practiceForms:['sentence-read','word-dictation','choice-exercise','role-play'],essay:{title:'The Value of Money',content:'Money plays an important role in society, but its true value is often misunderstood. Some believe money can buy happiness, while others argue love, friendship, and health cannot be purchased. We should view money as a tool to improve our lives and help others, rather than as the ultimate goal of life.'}},
};
function getUnitData(uk){return UNIT_CONTENT_DB[uk?.toLowerCase().replace(/\s/g,'')]||null;}
function findUnitData(book,unit){for(const[k,d]of Object.entries(UNIT_CONTENT_DB)){if(d.book===book&&d.unitName===unit)return{key:k,...d};}return null;}

const SK={searchHistory:'tx_sh',teachingProgress:'tx_tp',featureUsage:'tx_fu',resourceUsage:'tx_ru',assignedPractices:'tx_ap',dictationCards:'tx_dc',unitProgress:'tx_up',conversationHistory:'tx_ch'};
function ld(k,f){try{const r=localStorage.getItem(k);return r?JSON.parse(r):f;}catch(e){return f;}}
function sd(k,d){try{localStorage.setItem(k,JSON.stringify(d));}catch(e){}}
function gtp(){return ld(SK.teachingProgress,{className:'初一1班',book:'仁爱版七年级上册',unit:'Unit 1',unitName:'Making New Friends',lastTeachDate:'2026-05-20'});}
function utp(u){const c=gtp();sd(SK.teachingProgress,{...c,...u,lastTeachDate:new Date().toISOString().slice(0,10)});}
function rfu(id){const u=ld(SK.featureUsage,{});u[id]=(u[id]||0)+1;sd(SK.featureUsage,u);}
function rru(id){const u=ld(SK.resourceUsage,{});u[id]=(u[id]||0)+1;sd(SK.resourceUsage,u);}
function rs(q){const h=ld(SK.searchHistory,[]);h.unshift({query:q,time:Date.now()});if(h.length>50)h.length=50;sd(SK.searchHistory,h);}
function gap(){return ld(SK.assignedPractices,[]);}
function aap(p){const l=gap();l.unshift({...p,date:new Date().toISOString().slice(0,10),completed:Math.floor(Math.random()*30),total:48});sd(SK.assignedPractices,l);}
function sdc(c){const l=ld(SK.dictationCards,[]);l.unshift({...c,date:new Date().toISOString().slice(0,10)});sd(SK.dictationCards,l);}
function gup(uk){const a=ld(SK.unitProgress,{});return a[uk]||{started:null,accessCount:0,completedResources:[]};}
function rua(uk){const a=ld(SK.unitProgress,{});const c=a[uk]||{started:null,accessCount:0,completedResources:[]};c.accessCount=(c.accessCount||0)+1;if(!c.started)c.started=new Date().toISOString().slice(0,10);a[uk]=c;sd(SK.unitProgress,a);}
function cup(uk){const ud=getUnitData(uk);if(!ud)return 40;const up=gup(uk);const c=up.completedResources?up.completedResources.length:0;return Math.min(95,Math.round((c/ud.resources.length)*70+(up.accessCount||0)*5));}

const SM={'布置作业':'布置练习','留作业':'布置练习','改作业':'智能阅卷','批作业':'智能阅卷','背单词':'同步词汇','默写':'单词听写','PPT':'讲评课件','错题':'错题本','听力题':'听力材料'};
const AI=[...FUNCTION_DB,...RESOURCE_DB];
function ms(item,query){let s=0;const ql=query.toLowerCase();if(item.name===query)s+=15;if(item.name.includes(query))s+=8;if(query.includes(item.name))s+=10;if(item.desc.includes(query))s+=5;for(const kw of item.keywords){if(kw===query)s+=10;else if(kw.includes(query)||query.includes(kw))s+=7;else if(kw.toLowerCase().includes(ql))s+=6;}if(SM[query]){const t=SM[query];if(item.name===t)s+=8;}const tk=query.replace(/[，。！？、；：""''（）\s]+/g,' ').trim().split(' ').filter(Boolean);for(const t of tk){if(t.length<2)continue;if(item.name.includes(t))s+=4;for(const kw of item.keywords){if(kw.includes(t)||t.includes(kw))s+=3;}}return s;}
function si(query){return AI.map(i=>({...i,_score:ms(i,query)})).filter(i=>i._score>0).sort((a,b)=>b._score-a._score).slice(0,6);}
function eci(query){const info={classes:[],bookUnits:[]};const m1=query.match(/(初一|初二|初三|高一|高二|高三)\s*[（(]?\s*(\d+)\s*[）)]?\s*班?/);if(m1)info.classes.push(m1[0].replace(/[（()）]/g,''));const m2=query.match(/(必修\d+|选修\d+|仁爱版.*)/i);if(m2)info.bookUnits.push(m2[0]);return info;}
function eur(query){const m=query.match(/unit\s*(\d+)/i)||query.match(/第\s*(\d+)\s*单元/);if(m)return'unit'+m[1];const p=gtp();if(/找.*内容/.test(query)||/Unit.*(课文|词汇|课件)/.test(query)||/帮.*准备/.test(query)||/(课文|词汇|单词|跟读|听写)/.test(query))return p.unit.toLowerCase().replace(/\s/g,'');return null;}
function ewl(query){const c=query.replace(/[，。！？、；：""''（）()\s]+/g,',').replace(/^,|,$/g,'');const w=c.split(',').filter(w=>/^[a-zA-Z]+$/.test(w.trim()));return w.length>=2?w.map(w=>w.trim().toLowerCase()):null;}

const chatOverlay=document.getElementById('chatOverlay'),chatMessages=document.getElementById('chatMessages'),
      chatInput=document.getElementById('chatInput'),chatSend=document.getElementById('chatSend'),
      quickChips=document.getElementById('quickChips'),toast=document.getElementById('toast'),
      chatClose=document.getElementById('chatClose');
let isOpen=false;
function openChat(){isOpen=true;chatOverlay.classList.add('open');chatInput.focus();renderWelcome();window._lastSavedConv=null;}
function closeChat(){saveCurrentConversation();isOpen=false;chatOverlay.classList.remove('open');document.getElementById('historyDropdown').classList.remove('show');}
let tt;
function showToast(m){toast.textContent=m;toast.classList.add('show');clearTimeout(tt);tt=setTimeout(()=>toast.classList.remove('show'),2200);}
function sleep(ms){return new Promise(r=>setTimeout(r,ms));}

function renderMsg(role,text,opts={}){
  const{cards,recs,bubbleType,htmlExtras}=opts;
  const div=document.createElement('div'),bt=bubbleType||'normal';
  div.className=`msg ${role}${bt!=='normal'?' '+bt:''}`;
  const av=role==='assistant'?'✨':'👤';
  let h=`<div class="avatar">${av}</div><div class="bubble">${text}`;
  if(cards&&cards.length>0){h+='<div class="chat-cards">';cards.forEach(c=>{h+=`<div class="chat-card" data-action="${c.action||'open-resource'}" data-id="${c.id}" data-name="${c.name}"><div class="cc-icon ${c.iClass||'i-blue'}">${c.icon||'📌'}</div><div class="cc-info"><div class="cc-name">${c.name}</div><div class="cc-desc">${c.desc||''}</div></div><span class="cc-btn">点击使用 ›</span></div>`;});h+='</div>';}
  if(htmlExtras)h+=htmlExtras;
  h+='</div>';div.innerHTML=h;chatMessages.appendChild(div);chatMessages.scrollTop=chatMessages.scrollHeight;return div;
}
function renderTyping(){const d=document.createElement('div');d.className='msg assistant';d.id='typingIndicator';d.innerHTML='<div class="avatar">✨</div><div class="bubble"><div class="typing-dots"><span></span><span></span><span></span></div></div>';chatMessages.appendChild(d);chatMessages.scrollTop=chatMessages.scrollHeight;}
function removeTyping(){const e=document.getElementById('typingIndicator');if(e)e.remove();}

function getConversationHistory(){return ld(SK.conversationHistory,[]);}
function saveCurrentConversation(){const msgs=chatMessages.querySelectorAll('.msg');if(msgs.length===0)return;const html=chatMessages.innerHTML;if(html===window._lastSavedConv)return;window._lastSavedConv=html;const h=getConversationHistory();const t=extractConvTitle();h.unshift({id:Date.now(),title:t,html,time:new Date().toISOString()});if(h.length>20)h.length=20;sd(SK.conversationHistory,h);}
function extractConvTitle(){const msgs=chatMessages.querySelectorAll('.msg.user .bubble');if(msgs.length>0){const t=msgs[0].textContent.trim();return t.length>30?t.slice(0,30)+'…':t;}return'新对话';}

const GUIDE_CARDS=[
  {icon:'📖',text:'帮我找七年级上册Unit1的同步教学资源'},
  {icon:'🔊',text:'生成Unit1词汇的课堂领读内容'},
  {icon:'🎯',text:'帮我布置Unit1的听说专项练习'},
  {icon:'📊',text:'查看初一1班本周的练习完成情况'},
  {icon:'✏️',text:'帮我生成Unit1词汇听写答题卡'},
  {icon:'✍️',text:'给七年级学生写一篇My Friend的作文范文'},
  {icon:'📚',text:'基于当前教学进度推荐下一单元预习资源'},
  {icon:'🤖',text:'帮我批改学生的英语作文'},
  {icon:'📋',text:'一键查看待批阅的作业和未完成学生'},
];
function renderGuideCards(){
  const cardsHtml=GUIDE_CARDS.map(c=>`<div class="guide-card" data-guide-query="${c.text.replace(/"/g,'&quot;')}"><span class="gc-icon">${c.icon}</span><span class="gc-text">${c.text}</span></div>`).join('');
  return `<div class="guide-wrap"><div class="guide-title">有什么我能帮你的吗？</div><div class="guide-sub">点击下方卡片，快速开始使用小天智能助手</div><div class="guide-grid">${cardsHtml}</div></div>`;
}

function renderWelcome(){
  chatMessages.innerHTML='';
  const p=gtp(),uk=p.unit.toLowerCase().replace(/\s/g,'');rua(uk);
  const guideHtml=renderGuideCards();
  renderMsg('assistant','',{bubbleType:'guide-msg',htmlExtras:guideHtml});
  chatMessages.querySelectorAll('.guide-card').forEach(card=>{card.addEventListener('click',function(){const q=this.dataset.guideQuery;chatInput.value=q;handleUserMessage(q);});});
}

async function handleUserMessage(query){
  if(!query.trim())return;
  renderMsg('user',query);chatInput.value='';chatSend.disabled=true;rs(query);
  renderTyping();await sleep(400+Math.random()*400);removeTyping();
  const q=query.trim();let handled=false;
  const wl=ewl(q);if(wl&&!handled){handled=true;handleDictationFlow(wl);}
  if(!handled&&/学情|完成.*情况|作答|班级.*数据|查看.*完成/.test(q)){handled=true;handleStatsQuery();}
  const ur=eur(q);if(ur&&!handled){const ud=getUnitData(ur);if(ud){handled=true;handleUnitContentQuery(ud,q);}}
  if(!handled&&/专项练习|练习.*推送|帮我.*练习|准备.*练习/.test(q)){handled=true;handleStandardPracticeQuery(q);}
  if(!handled&&/布置|发布|安排.*练习/.test(q)){handled=true;handleAssignFlow(q);}
  if(!handled&&/推送.*单元|推送.*同步教学|推送.*资源/.test(q)){handled=true;handlePushResources(q);}
  if(!handled){const results=si(q),ci=eci(q);if(ci.classes.length>0||ci.bookUnits.length>0){const up={};if(ci.classes.length>0)up.className=ci.classes[0];if(ci.bookUnits.length>0)up.book=ci.bookUnits[0];utp(up);}if(results.length>0){renderMsg('assistant',`找到 ${results.length} 个相关内容：`,{cards:results.slice(0,4).map(r=>({...r,action:FUNCTION_DB.some(f=>f.id===r.id)?'open-feature':'open-resource'}))});}else{renderMsg('assistant','没有完全匹配的内容。试试说出单元名（如"Unit1"）、输入单词列表或功能名。',{cards:FUNCTION_DB.slice(0,3).map(f=>({...f,action:'open-feature'}))});}}
  chatSend.disabled=false;chatInput.focus();bindCardClicks();
}

function handleStatsQuery(){const ap=gap();renderMsg('assistant','近期班级练习作答情况：',{bubbleType:'resource-push',htmlExtras:`<div class="stats-push"><div class="sp-title">📊 班级学情</div><div class="sp-row"><span>已布置练习</span><span class="sp-val">${ap.length+8} 项</span></div><div class="sp-row"><span>平均完成率</span><span class="sp-val">92%</span></div><div class="sp-row"><span>未完成学生</span><span class="sp-val warn">${ap.reduce((s,a)=>s+(a.total-a.completed),0)||18} 人</span></div></div>`});}
function handleStandardPracticeQuery(query){const ur=eur(query)||gtp().unit.toLowerCase().replace(/\s/g,''),ud=getUnitData(ur)||Object.values(UNIT_CONTENT_DB)[0];rua(ur);utp({book:ud.book,unit:ud.unitName,unitName:ud.fullName});const pCards=[{id:'special-practice-res',name:'专项练习一：听说训练',desc:'主题听说·情景对话',icon:'🎧',iClass:'i-green',action:'open-resource'},{id:'special-practice-res',name:'专项练习二：听力理解',desc:'同步听力·信息提取',icon:'🎧',iClass:'i-green',action:'open-resource'},{id:'special-practice-res',name:'专项练习三：词汇巩固',desc:'核心词汇·语境运用',icon:'📚',iClass:'i-orange',action:'open-resource'},{id:'special-practice-res',name:'专项练习四：阅读理解',desc:'主题阅读·推理判断',icon:'📰',iClass:'i-teal',action:'open-resource'},{id:'special-practice-res',name:'专项练习五：写作训练',desc:'话题写作·范文参考',icon:'✍️',iClass:'i-purple',action:'open-resource'}];renderMsg('assistant',`为 <b>${ud.book} ${ud.unitName}</b> 推送专项练习与作文：`,{bubbleType:'resource-push',cards:pCards,htmlExtras:`<div class="chat-cards"><div class="chat-card" data-action="open-resource" data-id="writing-correction"><div class="cc-icon i-purple">📝</div><div class="cc-info"><div class="cc-name">作文：${ud.essay.title}</div><div class="cc-desc">${ud.essay.content.slice(0,50)}…</div></div><span class="cc-btn">查看全文 ›</span></div></div><div class="practice-options"><span class="practice-opt selected" style="cursor:pointer;" onclick="window._tx_quickAssignAll('${ur}')">📋 一键布置全部</span></div>`});}
window._tx_quickAssignAll=function(ur){showToast('✅ 已加入布置列表');setTimeout(()=>handleAssignFlow('布置练习 '+ur),400);};

function handleUnitContentQuery(ud,query){utp({book:ud.book,unit:ud.unitName,unitName:ud.fullName});rua(ud.unitName.toLowerCase().replace(/\s/g,''));const rc=ud.resources.map(rid=>{const r=RESOURCE_DB.find(x=>x.id===rid);return r?{...r,action:'open-resource'}:null;}).filter(Boolean);if(ud.themeVideos)ud.themeVideos.forEach(v=>rc.push({id:'theme-video-res',name:v.title,desc:v.desc,icon:'🎬',iClass:'i-pink',action:'open-resource'}));if(ud.currentReadings)ud.currentReadings.forEach(r=>rc.push({id:'current-reading-res',name:r.title,desc:r.desc,icon:'🌍',iClass:'i-teal',action:'open-resource'}));const vHtml=ud.vocab.map(w=>`<span class="word-chip vocab-sel-item" data-word="${w}" onclick="this.classList.toggle('selected');window._tx_updateReadingModal()">${w}</span>`).join('');const fOpts=ud.practiceForms.map(fid=>{const f=PRACTICE_FORMS.find(x=>x.id===fid);return f?`<span class="practice-opt" data-form-id="${f.id}" onclick="this.classList.toggle('selected')">${f.icon} ${f.name}</span>`:'';}).join('');renderMsg('assistant',`<b>${ud.book} ${ud.unitName} ${ud.fullName}</b> 完整内容：`,{bubbleType:'resource-push',cards:rc.slice(0,4),htmlExtras:`<div style="margin-top:8px;"><div style="font-size:11px;font-weight:600;">📖 ${ud.textTitle}</div><div style="font-size:10px;color:var(--text-muted);background:#F8FAFC;padding:6px 8px;border-radius:4px;line-height:1.5;">${ud.textFull.slice(0,150)}…</div><span style="font-size:10px;color:var(--primary);cursor:pointer;" onclick="window._tx_showFullText('${ud.unitName}')">查看完整课文 ›</span></div><div style="margin-top:8px;"><div style="font-size:11px;font-weight:600;display:flex;justify-content:space-between;"><span>📚 词汇 (${ud.vocab.length}个)</span><button class="pill sel" style="font-size:9px;cursor:pointer;" onclick="window._tx_openReadingModal('vocab','${ud.unitName}')">🔊 领读所选</button></div><div class="word-chips">${vHtml}</div></div><div style="margin-top:6px;font-size:10px;color:var(--text-muted);">需要生成本单元配套练习？</div><div class="practice-options">${fOpts}</div>${ud.essay?`<div style="margin-top:8px;"><div style="font-size:11px;font-weight:600;">✍️ ${ud.essay.title}</div><div style="font-size:10px;color:var(--text-muted);background:#F8FAFC;padding:6px 8px;border-radius:4px;">${ud.essay.content.slice(0,100)}…</div></div>`:''}`});window._currentReadingUnit=ud;}

function handleDictationFlow(words){sdc({words,mode:'mixed'});const wHtml=words.map(w=>`<span class="word-chip">${w}</span>`).join('');let tHtml='<table class="dc-table"><tr><th>#</th><th>英文</th><th>中文</th><th>听写区</th></tr>';words.forEach((w,i)=>{tHtml+=`<tr><td>${i+1}</td><td style="font-family:monospace;">${w}</td><td style="color:var(--text-muted);">___</td><td><input class="dc-input" placeholder="输入..." disabled></td></tr>`;});tHtml+='</table>';renderMsg('assistant',`识别到 <b>${words.length}</b> 个单词：`,{bubbleType:'resource-push',htmlExtras:`<div class="word-chips">${wHtml}</div><div class="dictation-card"><div class="dc-header"><span class="dc-title">📝 听写答题卡</span><span class="dc-mode" id="dictModeLabel">中英混合</span></div>${tHtml}<div style="margin-top:8px;font-size:10px;color:var(--text-muted);">听写模式：</div><div class="pill-row" style="margin-top:3px;" id="dictModeSelector"><span class="pill" data-mode="en">🇬🇧 英文</span><span class="pill" data-mode="cn">🇨🇳 中文</span><span class="pill sel" data-mode="mixed">🔀 混合</span></div><div class="dc-actions"><button onclick="this.closest('.dictation-card').style.display='none'">取消</button><button class="primary" onclick="window._tx_assignDictation(this)" data-words='${JSON.stringify(words)}'>确认并布置</button></div></div>`});}

function handleAssignFlow(query){const ci=eci(query),cls=ci.classes.length>0?ci.classes[0]:gtp().className,p=gtp(),sn=`${p.unit} ${p.unitName} 词汇听写`;renderMsg('assistant','请填写以下信息完成布置：',{bubbleType:'workflow-guide',htmlExtras:`<div class="assign-form" id="assignForm"><div class="af-section"><div class="afs-label">📝 练习名称</div><input class="af-input" id="afName" value="${sn}"></div><div class="af-section"><div class="afs-label">🎤 跟读模式</div><div class="pill-row" id="afReadMode"><span class="pill sel" data-val="single">单人跟读</span><span class="pill" data-val="pk">口语PK</span></div></div><div class="af-section"><div class="afs-label">📖 语篇练习形式</div><div class="pill-row" id="afTextMode"><span class="pill sel" data-val="sentence">逐句跟读</span><span class="pill" data-val="full">整篇跟读</span><span class="pill" data-val="recite">整篇背诵</span></div></div><div class="af-section"><div class="afs-label">🎯 达标线</div><div class="toggle-wrap"><div class="toggle-sw on" id="afThreshold" onclick="this.classList.toggle('on');document.getElementById('afThresholdLabel').textContent=this.classList.contains('on')?'已开启（≥80分）':'已关闭';"></div><span class="toggle-label" id="afThresholdLabel">已开启（≥80分）</span></div></div><div class="af-section"><div class="afs-label">📢 公布成绩</div><div class="pill-row" id="afPublish"><span class="pill sel" data-val="after">完成后公布</span><span class="pill" data-val="immediate">立即公布</span></div></div><div class="af-section"><div class="afs-label">👥 布置对象</div><div class="check-row" id="afTarget"><span class="check-item" onclick="this.querySelector('.ci-box').classList.toggle('checked')"><span class="ci-box checked"></span>初一1班</span><span class="check-item" onclick="this.querySelector('.ci-box').classList.toggle('checked')"><span class="ci-box checked"></span>初一3班</span><span class="check-item" onclick="this.querySelector('.ci-box').classList.toggle('checked')"><span class="ci-box"></span>初二5班</span></div></div><div class="af-section"><div class="afs-label">⏰ 开始时间</div><div class="pill-row" id="afStartTime"><span class="pill sel" data-val="now">立即开始</span><span class="pill" data-val="custom">指定时间</span></div></div><div class="af-section"><div class="afs-label">⏱️ 结束时间</div><div class="pill-row" id="afEndTime"><span class="pill sel" data-val="today2359">当天23:59</span><span class="pill" data-val="tomorrow2359">次日23:59</span><span class="pill" data-val="dayAfter2359">后天23:59</span><span class="pill" data-val="week">一周后</span><span class="pill" data-val="custom">自选</span></div></div><div class="af-section"><div class="afs-label">👁️ 可见时间</div><div class="pill-row" id="afVisible"><span class="pill sel" data-val="now">立即可见</span><span class="pill" data-val="start">开始时可见</span><span class="pill" data-val="custom">指定时间</span></div></div><div class="af-actions"><button class="af-btn-cancel" onclick="window._tx_cancelFullAssign()">取消</button><button class="af-btn-confirm" onclick="window._tx_confirmFullAssign()">确认布置</button></div></div>`});}

// 推送资源（展开式卡片）
function handlePushResources(query){
  const ur=eur(query)||gtp().unit.toLowerCase().replace(/\s/g,'');
  const ud=getUnitData(ur)||Object.values(UNIT_CONTENT_DB)[0];
  rua(ur);utp({book:ud.book,unit:ud.unitName,unitName:ud.fullName});

  const cards=[
    {id:'sync-text',name:'同步课文',icon:'📖',iClass:'i-blue',items:ud.vocab.slice(0,4).map((w,i)=>({id:w,label:`${ud.textTitle} — 第${i+1}段`,sub:ud.textFull.slice(i*40,(i+1)*40)+'…'})),btn:'🔊 逐句跟读',btnAction:'reading'},
    {id:'sync-vocab',name:'同步词汇',icon:'📚',iClass:'i-green',items:ud.vocab.slice(0,6).map(w=>({id:w,label:w,sub:(ud.vocabCN||{})[w]||'___'})),btns:[{label:'🔊 逐句跟读',action:'reading'},{label:'✏️ 单词听写',action:'dictation'}]},
    {id:'listening',name:'听力材料',icon:'🎧',iClass:'i-green',items:[{id:'l1',label:'Task 1: Listen and Choose',sub:'5道选择题'},{id:'l2',label:'Task 2: Listen and Fill',sub:'10个填空'},{id:'l3',label:'Task 3: Listen and Answer',sub:'3道问答题'}],btn:'🎧 开始听力练习',btnAction:'listening'},
    {id:'theme-video-res',name:'主题视频',icon:'🎬',iClass:'i-pink',items:(ud.themeVideos||[]).map(v=>({id:v.title,label:v.title,sub:v.desc+' · '+v.duration})),btn:'▶ 播放视频',btnAction:'video'},
  ];

  const cardsHtml=cards.map(c=>{
    const itemsHtml=c.items.map(it=>`<div class="ec-item" data-id="${it.id}" onclick="this.querySelector('.ec-check').classList.toggle('checked')"><span class="ec-check"></span><div style="flex:1;"><div style="font-weight:500;">${it.label}</div><div style="font-size:10px;color:var(--text-muted);">${it.sub||''}</div></div></div>`).join('');
    const btnsHtml=c.btns?c.btns.map(b=>`<button class="af-btn-confirm" onclick="window._tx_expandCardAction('${b.action}','${c.id}')">${b.label}</button>`).join(''):(c.btn?`<button class="af-btn-confirm" onclick="window._tx_expandCardAction('${c.btnAction}','${c.id}')">${c.btn}</button>`:'');
    return `<div class="expand-card" data-card-id="${c.id}">
      <div class="ec-header" onclick="this.parentElement.classList.toggle('open')">
        <div class="ec-hd-left"><span class="ec-hd-icon ${c.iClass}">${c.icon}</span><span class="ec-hd-name">${c.name}</span><span class="ec-hd-count">${c.items.length}项</span></div>
        <span class="ec-arrow">▾</span>
      </div>
      <div class="ec-body">${itemsHtml}</div>
      <div class="ec-footer">${btnsHtml}</div></div>`;
  }).join('');

  renderMsg('assistant',`为 <b>${ud.book} ${ud.unitName}</b> 推送以下教学资源：`,{bubbleType:'resource-push',htmlExtras:`<div style="margin-top:4px;">${cardsHtml}</div>`});
}

// 展开卡片按钮动作
window._tx_expandCardAction=function(action,cardId){
  const card=document.querySelector(`.expand-card[data-card-id="${cardId}"]`);
  const selected=[...card.querySelectorAll('.ec-item .ec-check.checked')].map(cb=>cb.parentElement.dataset.id);
  if(selected.length===0){showToast('请先勾选内容');return;}
  const ud=getUnitData(gtp().unit.toLowerCase().replace(/\s/g,''))||Object.values(UNIT_CONTENT_DB)[0];
  if(action==='reading'){window._currentReadingUnit=ud;window._tx_openReadingModal();window._tx_startReading();}
  else if(action==='dictation'){openFullscreenDictation(selected,ud);}
  else if(action==='listening'){openFullscreen('listeningPage');}
  else if(action==='video'){const v=ud.themeVideos?.find(v=>v.title===selected[0]);document.getElementById('videoPageTitle').textContent='🎬 '+(v? v.title:'主题视频');document.getElementById('videoPageDesc').textContent=v?v.desc:'视频播放区域';openFullscreen('videoPage');}
};

// 全屏页
function openFullscreen(id){document.getElementById(id).classList.add('open');}
window._tx_closeFullscreen=function(id){document.getElementById(id).classList.remove('open');};

// 全屏单词听写
let dictationWords=[],dictationIndex=0,dictationUnitData=null;
function openFullscreenDictation(words,ud){dictationWords=words;dictationIndex=0;dictationUnitData=ud;showDictationWord();openFullscreen('dictationPage');}
function showDictationWord(){if(dictationIndex>=dictationWords.length){showToast('听写完成！');window._tx_closeFullscreen('dictationPage');return;}const w=dictationWords[dictationIndex];document.getElementById('dictWord').textContent='🔊';document.getElementById('dictMeaning').textContent='请听发音并拼写单词';document.getElementById('dictInput').value='';document.getElementById('dictInput').focus();document.getElementById('dictInput').dataset.word=w;}
window._tx_nextDictationWord=function(){const w=document.getElementById('dictInput').dataset.word;const cn=dictationUnitData?.vocabCN||{};const answer=document.getElementById('dictInput').value.trim().toLowerCase();if(answer===w.toLowerCase()){showToast('✅ 正确！');}else{showToast(`正确答案：${w} (${cn[w]||''})`);}dictationIndex++;showDictationWord();};

// 练习选择弹窗（布置练习两步骤）
window._tx_openPracticeModal=function(unitName){
  const ud=getUnitData(unitName||gtp().unit.toLowerCase().replace(/\s/g,''))||Object.values(UNIT_CONTENT_DB)[0];
  document.getElementById('pmSub').textContent=`${ud.book} ${ud.unitName} — 选择要布置的练习`;
  const practices=[
    {id:'sync-practice',name:'同步练习',desc:'课文跟读 + 词汇巩固'},
    {id:'special-practice',name:'专项练习',desc:'听说 · 语法 · 阅读 · 写作'},
    {id:'vocab-dictation',name:'词汇听写',desc:`${ud.vocab.length}个核心词汇听写`},
    {id:'listening-practice',name:'听力练习',desc:'教材同步听力训练'},
  ];
  document.getElementById('pmList').innerHTML=practices.map(p=>`<div class="pm-item" data-pid="${p.id}" data-pname="${p.name}" onclick="this.parentElement.querySelectorAll('.pm-item').forEach(i=>i.classList.remove('sel'));this.classList.add('sel');"><span class="pm-radio"></span><div class="pm-info"><div class="pm-name">${p.name}</div><div class="pm-desc">${p.desc}</div></div></div>`).join('');
  document.getElementById('practiceModalOverlay').classList.add('open');
  window._pendingPracticeUnit=ud;
};
window._tx_closePracticeModal=function(){document.getElementById('practiceModalOverlay').classList.remove('open');};
window._tx_confirmPracticeSelect=function(){
  const sel=document.querySelector('#pmList .pm-item.sel');
  if(!sel){showToast('请先选择一项练习');return;}
  document.getElementById('practiceModalOverlay').classList.remove('open');
  const pname=sel.dataset.pname;
  showToast(`已选择「${pname}」，正在打开布置设置…`);
  setTimeout(()=>handleAssignFlow(`布置 ${pname}`),300);
};

// 首页布置练习按钮 → 打开练习选择弹窗
document.querySelectorAll('.func-btn').forEach(btn=>{btn.addEventListener('click',function(){window._tx_openPracticeModal();});});

// 领读
const readingOverlay=document.getElementById('readingOverlay');let readingMode='text',readingUnitData=null,readingPageIndex=0;window._currentReadingUnit=null;
window._tx_updateReadingModal=function(){const v=document.querySelectorAll('.vocab-sel-item.selected'),d=document.getElementById('readingModalDesc');if(d)d.textContent=`已选择 ${v.length} 个单词`;};
window._tx_openReadingModal=function(){window._tx_updateReadingModal();document.getElementById('readingModalOverlay').classList.add('open');};
window._tx_closeReadingModal=function(){document.getElementById('readingModalOverlay').classList.remove('open');};
window._tx_startReading=function(){document.getElementById('readingModalOverlay').classList.remove('open');readingUnitData=window._currentReadingUnit||Object.values(UNIT_CONTENT_DB)[0];readingMode='text';readingPageIndex=0;document.getElementById('readingTitle').textContent=`📖 ${readingUnitData.book} ${readingUnitData.unitName}`;renderReadingContent();readingOverlay.classList.add('open');showToast('全屏领读模式，适合课堂投屏');};
window._tx_closeReading=function(){readingOverlay.classList.remove('open');};
window._tx_toggleReadingMode=function(){readingMode=readingMode==='text'?'vocab':'text';document.getElementById('btnReadingMode').textContent=readingMode==='text'?'🔤 词汇模式':'📖 课文模式';readingPageIndex=0;renderReadingContent();};
function renderReadingContent(){const c=document.getElementById('readingContent');if(!readingUnitData)return;if(readingMode==='text'){c.innerHTML=`<div class="rc-text">${readingUnitData.textFull}</div>`;document.getElementById('readingProgress').textContent='课文模式';}else{const v=readingUnitData.vocab,cn=readingUnitData.vocabCN||{},ps=8,tp=Math.ceil(v.length/ps),st=readingPageIndex*ps,pv=v.slice(st,st+ps);c.innerHTML=`<div class="rc-vocab">${pv.map(w=>`<div class="rv-word"><div class="rv-english">${w}</div><div class="rv-chinese">${cn[w]||'___'}</div></div>`).join('')}</div>`;document.getElementById('readingProgress').textContent=`${readingPageIndex+1}/${tp}`;}}
window._tx_readingPrev=function(){if(readingMode==='vocab'&&readingPageIndex>0){readingPageIndex--;renderReadingContent();}};
window._tx_readingNext=function(){if(readingMode==='vocab'){const tp=Math.ceil((readingUnitData?.vocab||[]).length/8);if(readingPageIndex<tp-1){readingPageIndex++;renderReadingContent();}}};
window._tx_readingPlay=function(){const b=document.getElementById('btnPlay');b.textContent=b.textContent==='▶'?'⏸':'▶';};
window._tx_showFullText=function(un){const ud=getUnitData(un)||Object.values(UNIT_CONTENT_DB)[0];renderMsg('assistant',`<b>📖 ${ud.textTitle}</b>`,{htmlExtras:`<div style="background:#F8FAFC;padding:10px;border-radius:4px;font-size:11px;line-height:1.7;margin-top:4px;">${ud.textFull}</div><button class="pill sel" style="margin-top:6px;cursor:pointer;font-size:10px;" onclick="window._currentReadingUnit=getUnitData('${un}');window._tx_openReadingModal()">🔊 课堂领读</button>`});chatMessages.scrollTop=chatMessages.scrollHeight;};

// 布置
window._tx_cancelFullAssign=function(){const f=document.getElementById('assignForm');if(f)f.style.opacity='0.4';showToast('已取消');};
window._tx_confirmFullAssign=function(){const n=document.getElementById('afName')?.value||'练习';const gv=(id)=>{const e=document.getElementById(id);if(!e)return'';const s=e.querySelector('.pill.sel');return s?s.dataset.val:'';};const gc=(id)=>{const e=document.getElementById(id);if(!e)return[];return [...e.querySelectorAll('.check-item')].filter(it=>it.querySelector('.ci-box.checked')).map(it=>it.textContent.trim());};const rm=gv('afReadMode'),tm=gv('afTextMode'),th=document.getElementById('afThreshold')?.classList.contains('on'),pub=gv('afPublish'),tgs=gc('afTarget'),st=gv('afStartTime'),et=gv('afEndTime'),vis=gv('afVisible');const el={today2359:'当天23:59',tomorrow2359:'次日23:59',dayAfter2359:'后天23:59',week:'一周后',custom:'自选'},ml={sentence:'逐句跟读',full:'整篇跟读',recite:'整篇背诵'};aap({name:n,classId:tgs.join('、'),type:tm,readMode:rm,threshold:th?'≥80分':'关闭',publish:pub,startTime:st,endTime:et,visible:vis});const f=document.getElementById('assignForm');if(f)f.style.opacity='0.4';renderMsg('assistant','',{bubbleType:'workflow-guide',htmlExtras:`<div class="success-card"><div class="sc-check">✅</div><div class="sc-msg">布置成功！</div><div class="sc-detail"><b>${n}</b><br>班级：${tgs.join('、')}<br>模式：${rm==='single'?'单人跟读':'口语PK'} · ${ml[tm]||tm}<br>达标线：${th?'≥80分':'关闭'} · 成绩：${pub==='after'?'完成后公布':'立即公布'}<br>开始：${st==='now'?'立即':'指定'} · 截止：${el[et]||et} · 可见：${vis==='now'?'立即可见':vis==='start'?'开始时':'指定'}</div></div>`});chatMessages.scrollTop=chatMessages.scrollHeight;showToast('✅ 练习布置成功！');};
window._tx_assignDictation=function(btn){const w=JSON.parse(btn.dataset.words),me=document.querySelector('#dictModeSelector .pill.sel'),m=me?me.dataset.mode:'mixed',ml={en:'英文听写',cn:'中文听写',mixed:'中英混合'};aap({name:`单词听写 (${w.length}词)`,classId:'初一1班',type:'dictation'});sdc({words:w,mode:m});showToast('✅ 答题卡已生成！');const c=btn.closest('.dictation-card');if(c)c.style.opacity='0.5';};
window._tx_urgePractice=function(n){showToast(`📢 已发送催促通知${n!=='all'?`：「${n}」`:''}`);};
window._tx_viewReport=function(n){showToast(`✅ 跳转到${n!=='all'?`「${n}」`:''}练习报告…`);};

function bindCardClicks(){chatMessages.querySelectorAll('.chat-card').forEach(c=>{c.addEventListener('click',function(){const a=this.dataset.action,id=this.dataset.id,n=this.dataset.name;if(a==='open-feature'){rfu(id);showToast(`✅ 跳转到「${n}」…`);}else if(a==='open-resource'){rru(id);showToast(`✅ 打开「${n}」…`);}});});}

document.addEventListener('click',function(e){const p=e.target.closest('.pill');if(p&&p.parentElement.classList.contains('pill-row')){p.parentElement.querySelectorAll('.pill').forEach(o=>o.classList.remove('sel'));p.classList.add('sel');}if(e.target.closest('#dictModeSelector')){const s=e.target.closest('.pill');if(s){s.parentElement.querySelectorAll('.pill').forEach(o=>o.classList.remove('sel'));s.classList.add('sel');const ml={en:'英文听写',cn:'中文听写',mixed:'中英混合'},l=document.getElementById('dictModeLabel');if(l)l.textContent=ml[s.dataset.mode]||'中英混合';}}});

// 事件绑定
document.getElementById('aiEntryCard').addEventListener('click',openChat);
document.getElementById('smartSearchEntry').addEventListener('click',openChat);
document.getElementById('bbAiToggle').addEventListener('click',openChat);
chatClose.addEventListener('click',closeChat);
chatOverlay.addEventListener('click',function(e){if(e.target===chatOverlay)closeChat();});
chatSend.addEventListener('click',()=>handleUserMessage(chatInput.value));
chatInput.addEventListener('keydown',function(e){if(e.key==='Enter'){e.preventDefault();handleUserMessage(chatInput.value);}if(e.key==='Escape')closeChat();});
document.addEventListener('keydown',function(e){if((e.ctrlKey||e.metaKey)&&e.key==='k'){e.preventDefault();isOpen?closeChat():openChat();}});
quickChips.addEventListener('click',function(e){const chip=e.target.closest('.quick-chip');if(!chip)return;chatInput.value=chip.dataset.query;handleUserMessage(chip.dataset.query);});
document.getElementById('btnNewChat').addEventListener('click',function(e){e.stopPropagation();saveCurrentConversation();renderWelcome();showToast('已开启新对话');});
document.getElementById('btnHistory').addEventListener('click',function(e){e.stopPropagation();const dd=document.getElementById('historyDropdown');const h=getConversationHistory();if(h.length===0){dd.innerHTML='<div class="hd-empty">暂无历史对话</div>';}else{dd.innerHTML=h.map((h,i)=>`<div class="hd-item" data-idx="${i}"><div style="font-weight:600;margin-bottom:2px;">${h.title}</div><div style="font-size:10px;color:var(--text-muted);">${new Date(h.time).toLocaleString('zh-CN')}</div></div>`).join('');dd.querySelectorAll('.hd-item').forEach(item=>{item.addEventListener('click',function(ev){ev.stopPropagation();const idx=parseInt(this.dataset.idx);const h=getConversationHistory()[idx];if(h){chatMessages.innerHTML=h.html;bindCardClicks();showToast('已加载历史对话');}dd.classList.remove('show');});});}dd.classList.toggle('show');});
document.addEventListener('click',function(e){if(!e.target.closest('#btnHistory')&&!e.target.closest('#historyDropdown')){document.getElementById('historyDropdown').classList.remove('show');}});
document.getElementById('readingModalOverlay').addEventListener('click',function(e){if(e.target===this)window._tx_closeReadingModal();});

// 侧边栏导航切换
document.querySelectorAll('.sb-nav-item').forEach(item=>{item.addEventListener('click',function(){document.querySelectorAll('.sb-nav-item').forEach(i=>i.classList.remove('active'));this.classList.add('active');});});

// 初始化
function init(){
  const fU=ld(SK.featureUsage,{});
  if(Object.keys(fU).length===0){
    sd(SK.featureUsage,{'sync-teach':15,'special-practice':10,'mock-exam':6,'fun-dubbing':8,'current-reading':5,'assign-practice':12});
    sd(SK.searchHistory,[{query:'布置同步练习 初一1班',time:Date.now()-86400000}]);
    sd(SK.assignedPractices,[{name:'Unit1 词汇听写练习',classId:'初一1班',type:'单词听写',date:'2026-05-14',completed:41,total:48},{name:'Unit1 同步课文跟读',classId:'初一1班',type:'逐句跟读',date:'2026-05-10',completed:31,total:48},{name:'Unit1 听说专项练习',classId:'初一3班',type:'听说练习',date:'2026-05-08',completed:20,total:48}]);
    sd(SK.unitProgress,{unit1:{started:'2026-05-01',accessCount:8,completedResources:['sync-text','sync-vocab']}});
  }
}
init();
})();
</script>
</body>
</html>
