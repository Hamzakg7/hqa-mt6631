<!--
═══════════════════════════════════════════════════════════
  HQA Protocol — MediaTek MT6631 Research
  From Syria, from the dark 🇸🇾

  Author: Hamzakg7
  Date: 2026-10-13

  ⚠️ Educational research only
═══════════════════════════════════════════════════════════
-->

<div align="center">

# HQA Protocol — MediaTek MT6631

### اكتشاف بروتوكول مخفي في شريحة WiFi

### Discovery of a hidden protocol in MediaTek WiFi chip

---

**From Syria, from the dark 🇸🇾**

**من سوريا، من الظلام 🇸🇾**

---

[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Chip](https://img.shields.io/badge/Chip-MediaTek%20MT6631-red.svg)]()
[![Status](https://img.shields.io/badge/Status-Research-orange.svg)]()
[![Community](https://img.shields.io/badge/Community-Welcome-blue.svg)]()

</div>

---

## 🌍 من سوريا، من الظلام

<div dir="rtl">

من سوريا، من الظلام.

7 أيام. بدون كهربا. بدون أدوات.
بس فلاش الجوال وورقة وقلم.

فتحت كيرنل أندرويد كامل.
ولقيت بروتوكول مخفي اسمه HQA.
غير موجود في أي توثيق رسمي.

هذا المستودع مو شرح كامل.
هذا دعوة للمجتمع.

أنا لقيت الباب وفتحته.
الباقي عليكم.

</div>

**In English:**

> From Syria, from the dark.
>
> 7 days. No electricity. No tools.
> Just phone flashlight, paper, and pen.
>
> I opened the full Android kernel.
> And found a hidden protocol called HQA.
> Not in any official documentation.
>
> This is not a complete guide.
> This is an invitation to the community.
>
> I found the door and opened it.
> The rest is up to you.

---

## 💡 لماذا هذا المستودع؟

<div dir="rtl">

أنا ما راح أعطيك كل شي جاهز.

أنا راح أعطيك:
- ✅ الأوامر اللي لقيتها
- ✅ البنية اللي فهمتها
- ✅ المسار اللي اكتشفته
- ✅ الدلائل اللي جمعتها

وأنت تكمل:

- 🎯 تفهم الكود
- 🎯 تطور الأدوات
- 🎯 تكتشف المزيد
- 🎯 تشارك المجتمع

هذا البحث مفتوح.
الباب مفتوح.
شاركنا.

</div>

**In English:**

> I'm not giving you everything ready-made.
>
> I'm giving you:
> - ✅ The commands I found
> - ✅ The structures I understood
> - ✅ The path I discovered
> - ✅ The proof I collected
>
> And you continue:
>
> - 🎯 Understand the code
> - 🎯 Develop the tools
> - 🎯 Discover more
> - 🎯 Share with community
>
> This research is open.
> The door is open.
> Join us.

---

## ⚠️ تنبيه مهم

<div dir="rtl">

هذا البحث تجريبي بالكامل.

أنا لا أتحمل أي مسؤولية عن أي أضرار أو أعطال أو استخدامات غير قانونية.

- 🚫 الاستخدام على شبكة الآخرين جريمة
- ⚠️ الاستخدام الخاطئ قد يحرق شريحة WiFi
- ⚠️ الاستخدام الخاطئ قد يعطب جهازك

</div>

**In English:**

> This is experimental research.
>
> I take NO responsibility for any damage or misuse.
>
> - 🚫 Use on other networks is illegal
> - ⚠️ Wrong use may burn your WiFi chip
> - ⚠️ Wrong use may brick your device

---

## 🎯 الهدف

<div dir="rtl">

بالعربي:

- مشاركة المعرفة التقنية
- تشجيع الباحثين العرب
- بناء مجتمع أمني سوري
- فتح الباب للجيل القادم
- إثبات أن العرب يقدروا يبتكروا

رسالة من القلب:

يا شباب العرب — لا تستسلموا.
الظروف الصعبة تصنع عقول قوية.
لو أنا قدرت من سوريا، من الظلام...
أنتم كمان تقدروا.

</div>

**In English:**

> Purpose:
>
> - Share technical knowledge
> - Encourage Arab researchers
> - Build a Syrian security community
> - Open the door for the next generation
> - Prove that Arabs can innovate
>
> A message from the heart:
>
> To all Arab youth — don't give up.
> Hard conditions create strong minds.
> If I could do it from Syria, from the dark...
> You can too.

---

## ✅ النتيجة

<div dir="rtl">

- ✅ Monitor Mode على MT6631
- ✅ استقبال إطارات كامل من radiotap0
- ✅ إرسال إطارات Beacon (حقن حزم)
- ✅ تحكم كامل بالشريحة

</div>

**In English:**

- ✅ Monitor Mode on MT6631
- ✅ Full frame reception from radiotap0
- ✅ Beacon frame injection
- ✅ Full chip control

---

## 🔬 الدليل الأول: Monitor Mode

**المصدر:** gl_init.c

```c
// Line 162
#define NIC_MONITOR_INF_NAME "radiotap%d"

// Line 2335
static int wlanMonOpen(struct net_device *prDev) {
    netif_tx_start_all_queues(prDev);
    return 0;
}

// Line 2388
prGlueInfo->prMonDevHandler->type = ARPHRD_IEEE80211_RADIOTAP;
```

**التفعيل:**

```bash
echo "MONITOR 1 6 20 0" > /proc/net/wlan/driver
ip link set radiotap0 up
```

**يستدعي:** priv_driver_set_monitor() في gl_wext_priv.c:11443

---

## 🔬 الدليل الثاني: بروتوكول HQA

**المصدر:** wlan_service/agent/agent.c

```c
// Line 132
struct GNU_PACKED hqa_frame {
    u_int32 magic_no;    // 0x18142880
    u_int16 type;        // 0x0005 (REQ) / 0x8005 (RSP)
    u_int16 id;          // Command
    u_int16 length;
    u_int16 sequence;
    u_int8  data[4084];
};

// Line 30
#define TEST_CMD_MAGIC_NO  0x18142880
```

**المدخل:**

```c
// gl_wext.c:281
[IOCTL_QA_TOOL_DAEMON - SIOCIWFIRSTPRIV] = priv_qa_agent

IOCTL_QA_TOOL_DAEMON = SIOCIWFIRSTPRIV + 16
                     = 0x8BE0 + 16 = 0x8BF0
```

---

## 🔬 الدليل الثالث: جداول الأوامر

**المصدر:** gl_qa_agent.c

```c
// Line 9396
static struct HQA_CMD_TABLE HQA_CMD_TABLES[] = {
    { HQA_CMD_SET0, ..., 0x1000 },
    { HQA_CMD_SET1, ..., 0x1100 },
    { HQA_CMD_SET2, ..., 0x1200 },
    { HQA_CMD_SET3, ..., 0x1300 },
    { HQA_CMD_SET4, ..., 0x1400 },
    { HQA_CMD_SET5, ..., 0x1500 },
    { HQA_CMD_SET6, ..., 0x1600 },
};

// Line 9306
static HQA_CMD_HANDLER hqa_ext_cmd_set[] = {
    NULL,
    hqa_set_channel_ext,    // 0x00000001
    hqa_set_txcontent_ext,  // 0x00000002
    hqa_start_tx_ext,       // 0x00000003
    hqa_start_rx_ext,       // 0x00000004
    hqa_stop_tx_ext,        // 0x00000005
    hqa_stop_rx_ext,        // 0x00000006
    ...
};
```

---

## 🔬 الدليل الرابع: دالة الإرسال

**المصدر:** gl_qa_agent.c:8706

```c
static int32_t hqa_start_tx_ext(...) {
    memcpy(&u4Pkt_cnt, Data + 4*3, 4);   // Packet count
    memcpy(&u4Phymode, Data + 4*4, 4);   // PHY mode
    memcpy(&u4Rate,    Data + 4*5, 4);   // Rate
    memcpy(&u4Pwr,     Data + 4*6, 4);   // Power

    MT_ATESetDBDCBandIndex(prNetDev, u4Band_idx);
    MT_ATESetTxCount(prNetDev, u4Pkt_cnt);
    MT_ATESetRate(prNetDev, u4Rate);
    MT_ATESetTxPower0(prNetDev, u4Pwr);

    MT_ATEStartTX(prNetDev, "TXFRAME");
}
```

---

## 📊 كل الأوامر اللي اكتشفتها

<div dir="rtl">

هذه كل الأوامر اللي لقيتها في الكيرنل:

</div>

### 🎯 HQA Commands

| Command | ID | Description |
|---|---|---|
| HQA OpenAdapter | 0x1000 | فتح المحول |
| HQA CloseAdapter | 0x1001 | إغلاق المحول |
| HQA SetTxPath | 0x100B | مسار الإرسال |
| HQA SetRxPath | 0x100C | مسار الاستقبال |
| HQA SetChannel | 0x1100 | ضبط القناة |
| HQA SetPreamble | 0x1101 | Preamble |
| HQA SetRate | 0x1102 | المعدل |
| HQA SetNss | 0x1103 | NSS |
| HQA SetSystemBW | 0x1104 | عرض النطاق |
| HQA MacBbpRegRead | 0x1300 | قراءة سجل |
| HQA MacBbpRegWrite | 0x1301 | كتابة سجل |
| HQA GetChipID | 0x1514 | معرّف الشريحة |
| HQA GetTxInfo | 0x1313 | معلومات الإرسال |

### 🎯 DBDC Commands (0x1600)

| Command | Sub-ID | Description |
|---|---|---|
| HQA DBDCSetChannel | 1 | ضبط القناة |
| HQA DBDCSetTXContent | 2 | محتوى الإطار |
| HQA DBDCStartTX | 3 | بدء الإرسال |
| HQA DBDCStartRX | 4 | بدء الاستقبال |
| HQA DBDCStopTX | 5 | إيقاف الإرسال |
| HQA DBDCStopRX | 6 | إيقاف الاستقبال |

### 🎯 MPS Commands

| Command | ID | Description |
|---|---|---|
| MPSSetSeqData | 0x1515 | بيانات الإطار |
| MPSSetPayloadLength | 0x1516 | طول الحمولة |
| MPSSetPacketCount | 0x1517 | عدد الحزم |
| MPSSetPowerGain | 0x1518 | قوة الإرسال |
| MPSStart | 0x1519 | بدء الإرسال |
| MPSStop | 0x151A | إيقاف الإرسال |

---

## 🎬 الأوامر الحقيقية اللي اشتغلت

```bash
# 1. Open Adapter
iwpriv wlan0 driver "HQA OpenAdapter"
# → wlan0 driver:Return : 0x0000

# 2. Set Channel 6
iwpriv wlan0 driver "HQA DBDCSetChannel=1,11,0,6,0,0,0,0,0,0,2437"
# → wlan0 driver:Return : 0x0000
# → ExtId : 0x00000001

# 3. Set TX Content (Beacon)
iwpriv wlan0 driver "HQA DBDCSetTXContent=2,12,0,0x8000,0,0,0,100,100,ff:ff:ff:ff:ff:ff,06:7a:ab:de:c1:5e,06:7a:ab:de:c1:5e"
# → wlan0 driver:Return : 0x0000
# → ExtId : 0x00000002

# 4. Start TX
iwpriv wlan0 driver "HQA DBDCStartTX=3,17,0,100,0,0,20,0,0,0,0,0,0,0,0,0,0,0"
# → wlan0 driver:Return : 0x0000
# → ExtId : 0x00000003

# 5. Check Result
iwpriv wlan0 driver "HQA GetTxInfo"
# → Band0 TX : 0x00000064
```

**`0x64` = 100 حزمة أرسلت فعليا.** ✅

---

## 🧠 المسار التقني

```
IOCTL_QA_TOOL_DAEMON = 0x8BF0
    ↓
priv_qa_agent()
    ↓
mt_agent_hqa_cmd_handler()
    ↓
mt_agent_hqa_cmd_string_parser()
    ↓
priv_hqa_cmd_mapping[]
    ↓
HQA_CMDHandler()
    ↓
hqa_ext_cmds()
    ↓
hqa_ext_cmd_set[]
    ↓
hqa_set_channel_ext
hqa_set_txcontent_ext
hqa_start_tx_ext
    ↓
MT_ATEStartTX("TXFRAME")
    ↓
Hardware
```

---

## 💬 رسالة للمجتمع

<div dir="rtl">

أنا ما راح أعطيكم كل شي جاهز.
هذا الباب.
ادخلوا واكملوا.

**نصيحة:**

- اقرأوا الكود قبل التنفيذ
- افهموا الأوامر قبل التجربة
- استخدموا مختبر معزول
- احترموا القانون
- احترموا خصوصية الآخرين

**كلمة للعرب:**

يا شباب — إحنا مو أقل من غيرنا.
الظروف صعبة، بس العقل ما يعرف ظروف.
لو أنا قدرت من سوريا، من الظلام...
أنتم كمان تقدروا.

**كلمة للأجانب:**

This research comes from a place of war.
From a country where electricity is a luxury.
From a young researcher who just wanted to learn.

If we can do it, anyone can.
And if you can improve it, please share.

</div>

**In English:**

> I'm not giving you everything ready-made.
> This is the door.
> Walk in and continue.
>
> **Advice:**
>
> - Read code before running
> - Understand commands before testing
> - Use an isolated lab
> - Respect the law
> - Respect others' privacy
>
> **A word to the Arabs:**
>
> We are not less than anyone.
> Conditions are hard, but the mind doesn't know conditions.
> If I could do it from Syria, from the dark...
> You can too.
>
> **A word to the world:**
>
> This research comes from a place of war.
> From a country where electricity is a luxury.
> From a young researcher who just wanted to learn.
>
> If we can do it, anyone can.
> And if you can improve it, please share.

---

## ❓ أسئلة مفتوحة للمجتمع

<div dir="rtl">

أنا ما عندي كل الأجوبة.

هذا اللي لسه ما عرفته:

- 🎯 كيف نضيف Payload مخصص؟
- 🎯 كيف نبني إطار Beacon كامل مع SSID؟
- 🎯 كيف نرسل أنواع إطارات ثانية؟
- 🎯 كيف نوسع الأدوات؟
- 🎯 كيف نبني مجتمع أمني عربي؟

هذا الباب اللي فتحته.
الباقي عليكم.

</div>

**In English:**

> I don't have all the answers.
>
> This is what I don't know yet:
>
> - 🎯 How to inject custom Payload?
> - 🎯 How to build a full Beacon frame with SSID?
> - 🎯 How to send other frame types?
> - 🎯 How to expand the tools?
> - 🎯 How to build an Arab security community?
>
> This is the door I opened.
> The rest is up to you.

---

## 📜 License

**MIT License** — see [LICENSE](LICENSE)

---

<div align="center">

## 💙 أحبكم يا جماعة

**شكراً لكل واحد قرأ.**
**شكراً لكل واحد شارك.**
**شكراً لكل واحد آمن إن العرب يقدروا.**

**هذا البحث مو ملكي.**
**هذا البحث ملك كل واحد يبغى يتعلم.**

---

**لو حبيت البحث:**

⭐ اضغط Star — بكفي
🍴 اعمل Fork — وطوّر
💬 شارك فكرة — وخلينا نكبر

**معاً — نبني مجتمع تقني عربي قوي.**

---

**In English:**

## 💙 Much Love to Everyone

**Thanks to everyone who read.**
**Thanks to everyone who shared.**
**Thanks to everyone who believed Arabs can do it.**

**This research is not mine.**
**This research belongs to anyone who wants to learn.**

---

**If you liked this:**

⭐ Press Star — that's enough
🍴 Fork it — and improve
💬 Share an idea — let's grow

**Together — we build a strong Arab tech community.**

---

**Follow:** [@Hamzakg7](https://github.com/Hamzakg7)

---

**من سوريا، من الظلام. 🇸🇾**

**From Syria, from the dark. 🇸🇾**

---

> *"العلم نور، والجهل ظلام"*
> *"Knowledge is light, ignorance is darkness"*

---

**Made with 💙 in Syria**

</div>