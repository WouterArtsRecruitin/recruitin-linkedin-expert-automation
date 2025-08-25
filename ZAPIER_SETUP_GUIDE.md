# 🔗 Zapier Integration Setup Guide

## 🎯 Doel
Automatische verwerking van LinkedIn Expert audit aanvragen via Zapier workflows.

## 🚨 Huidige Status
❌ **Mock Webhook URL**: `https://hooks.zapier.com/hooks/catch/123456/linkedin-lead/`
✅ **Form werkt**: JSON response bevestigd
❌ **Workflow actief**: Leads worden niet verder verwerkt

## 🔧 Setup Instructies

### Stap 1: Zapier Webhook Setup (5 minuten)

1. **Ga naar Zapier**: https://zapier.com/app/editor
2. **Create Zap**: "Webhooks by Zapier" als trigger
3. **Trigger Event**: "Catch Hook" 
4. **Get URL**: Kopieer de echte webhook URL
5. **Test webhook**: Gebruik de form om test data te versturen

### Stap 2: Vervang Mock URL (1 minuut)

**Huidige code** (regel 339 in landing_page.html):
```html
<form class="lead-form" action="https://hooks.zapier.com/hooks/catch/123456/linkedin-lead/" method="POST">
```

**Vervang met je echte Zapier URL**:
```html
<form class="lead-form" action="https://hooks.zapier.com/hooks/catch/JOUW_WEBHOOK_ID/linkedin-lead/" method="POST">
```

### Stap 3: Zapier Workflow Acties

Voeg deze acties toe aan je Zapier workflow:

#### ✉️ **Email Notifications**
- **App**: Gmail/Outlook
- **Action**: Send Email  
- **To**: `info@recruitin.nl`
- **Subject**: `🎯 Nieuwe LinkedIn Audit Aanvraag - {{name}}`
- **Body Template**:
```
Nieuwe LinkedIn Expert audit aanvraag ontvangen!

📋 LEAD DETAILS:
Naam: {{name}}
Email: {{email}}  
LinkedIn URL: {{linkedin_url}}
Experience Level: {{experience_level}}
Tech Stack: {{tech_stack}}
Grootste Uitdaging: {{challenge}}
Interesse in Pakket: {{package}}

🎯 AUDIT ID: {{zap_meta_human_now}}
⏰ Ontvangen: {{zap_meta_timestamp}}

ACTIE VEREIST:
1. Analyseer LinkedIn profiel binnen 24 uur
2. Verstuur persoonlijke audit rapport  
3. Plan follow-up gesprek indien gewenst

Direct contact: {{email}}
```

#### 📊 **CRM Integration (Optioneel)**
- **App**: HubSpot/Pipedrive/Google Sheets
- **Action**: Create Contact/Deal
- **Map fields**: Naam, email, LinkedIn URL, etc.

#### 📱 **Slack/Teams Notification (Optioneel)**  
- **App**: Slack/Microsoft Teams
- **Action**: Send Message
- **Channel**: #leads of #recruitment
- **Message**: `🎯 Nieuwe LinkedIn audit: {{name}} ({{experience_level}})`

### Stap 4: Test Complete Flow

1. **Vul formulier in**: Op je live site
2. **Check Zapier**: Verify webhook received data  
3. **Check email**: Bevestig notification ontvangen
4. **Check CRM**: Verify contact/deal created
5. **Test success page**: Verify redirect works

## 🎯 Expected Data Format

Je Zapier webhook ontvangt deze velden:

```json
{
  "name": "Jan de Vries",
  "email": "jan@example.com", 
  "linkedin_url": "https://linkedin.com/in/jandevries",
  "experience_level": "Senior",
  "tech_stack": "React, Node.js, AWS",
  "challenge": "Te weinig views en connecties",
  "package": "authority"
}
```

## 🚀 Advanced Workflows

### Multi-Step Nurturing Sequence
1. **Immediate**: Welcome email met audit timeline
2. **24 hours**: Audit rapport delivery via email
3. **48 hours**: Follow-up voor feedback/vragen  
4. **1 week**: Sales follow-up voor pakket upgrade

### Lead Scoring
- **Hot Lead** (Premium interesse): Direct phone call
- **Warm Lead** (Authority Builder): Email sequence
- **Cold Lead** (Foundation only): Automated email

### Integration Opties
- **ActiveCampaign**: Email marketing automation
- **Calendly**: Automatische meeting scheduling
- **WhatsApp**: Direct messaging voor hot leads
- **Google Sheets**: Lead tracking en reporting

## 🔍 Troubleshooting

### Form submits maar geen Zapier data
1. Check webhook URL is correct (niet de mock URL)
2. Verify Zapier zap is turned ON
3. Check Zapier task history for errors

### JSON response maar geen email
1. Check Gmail/Outlook integration in Zapier
2. Verify email template is correct
3. Check spam folder voor notifications

### Success page niet werkend
1. Check JavaScript console voor errors
2. Verify success.html is deployed to Netlify
3. Test direct access to /success.html

## 📊 Monitoring & Analytics

### Zapier Dashboard
- Monitor task usage en success rate
- Track webhook performance
- Review error logs monthly

### Lead Quality Tracking
- Response rates per lead source
- Conversion rates by experience level  
- Package preference analysis

---

## ✅ Implementation Checklist

- [ ] Create real Zapier webhook (replace mock URL)
- [ ] Configure email notifications to info@recruitin.nl
- [ ] Set up CRM integration (optional)
- [ ] Test complete form → email → CRM flow
- [ ] Verify success page redirect works  
- [ ] Configure lead scoring/routing logic
- [ ] Set up monitoring and alerts
- [ ] Document process voor team

**Status**: Ready for production implementation
**ETA**: 15-30 minuten setup tijd
**ROI**: Automatische lead processing = 5+ uren per week besparing