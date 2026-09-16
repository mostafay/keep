# Keep Backend Server

سيرفر Node.js لاستخراج الصور من المواقع وحفظها في Cloudinary.

## المميزات

- استخراج أكبر صورة من أي موقع ويب
- رفع الصور تلقائياً إلى Cloudinary
- واجهة API بسيطة للاستخدام

## التثبيت

1. تثبيت التبعيات:
```bash
npm install
```

2. إنشاء ملف `.env` بناءً على `.env.example`:
```bash
cp .env.example .env
```

3. إعداد Cloudinary:
- سجل في [Cloudinary](https://cloudinary.com/)
- احصل على Cloud Name, API Key, و API Secret من لوحة التحكم
- أضفها إلى ملف `.env`

## التشغيل

```bash
npm start
```

للتطوير مع إعادة التشغيل التلقائي:
```bash
npm run dev
```

## استخدام API

### استخراج وحفظ صورة

أرسل طلب POST إلى `/extract-image` مع JSON يحتوي على URL:

```bash
curl -X POST http://localhost:3000/extract-image \
  -H "Content-Type: application/json" \
  -d '{"url": "https://watch.plex.tv/show/bodies"}'
```

الرد سيكون:
```json
{
  "success": true,
  "originalImageUrl": "https://...",
  "cloudinaryUrl": "https://res.cloudinary.com/...",
  "publicId": "extracted-images/...",
  "width": 1920,
  "height": 1080
}
```

### فحص صحة السيرفر

```bash
curl http://localhost:3000/health
```

## كيف يعمل

1. السيرفر يستقبل URL من العميل
2. يستخدم Axios و Cheerio لاستخراج HTML من الصفحة
3. يبحث عن جميع الصور في الصفحة
4. يختار أكبر صورة بناءً على الأبعاد
5. يرفع الصورة إلى Cloudinary
6. يرجع رابط الصورة في Cloudinary للعميل

## التبعيات

- express: إطار عمل الويب
- axios: لطلب HTTP
- cheerio: لتحليل HTML
- cloudinary: SDK للتعامل مع Cloudinary
- cors: للتعامل مع CORS
- dotenv: لإدارة المتغيرات البيئية
