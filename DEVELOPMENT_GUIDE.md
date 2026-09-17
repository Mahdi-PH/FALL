# 🛠️ دليل التطوير والنصائح العملية

## 1. إعداد بيئة التطوير

### خطوات البدء الأساسية

#### الخطوة 1: تثبيت Unity
```bash
# تنزيل Unity Hub
# ثم تثبيت Unity 2022 LTS أو أحدث
# تثبيت المكونات الإضافية:
# - IL2CPP Scripting Backend
# - Android Build Support (إذا كنت تستهدف الهاتف)
# - Windows Build Support
```

#### الخطوة 2: استنساخ المشروع
```bash
git clone https://github.com/Mahdi-PH/FALL.git
cd FALL
git checkout claude/3d-game-development-plan-g9n3fe
```

#### الخطوة 3: إعداد Git
```bash
git config user.name "اسمك"
git config user.email "بريدك@example.com"
```

#### الخطوة 4: فتح المشروع في Unity
```
File → Open Project → اختر مجلد FALL
```

---

## 2. الممارسات الأفضل للترميز

### معايير الكود

#### 1. الأسماء الواضحة
```csharp
// ✗ سيء
private float h, d, r;

// ✓ جيد
private float health, damage, regenerationRate;
```

#### 2. استخدم SOLID Principles
```csharp
// ✓ Single Responsibility
public class HealthSystem : MonoBehaviour
{
    // مسؤول فقط عن الصحة
}

public class HealthDisplay : MonoBehaviour
{
    // مسؤول فقط عن عرض الصحة
}
```

#### 3. استخدم Events بدلاً من Callbacks
```csharp
// ✗ سيء
private PlayerController player;
private void Update()
{
    if (player.isDead)
        OnPlayerDeath();
}

// ✓ جيد
private void Start()
{
    PlayerHealth health = FindObjectOfType<PlayerHealth>();
    health.OnDeath += HandlePlayerDeath;
}
```

#### 4. تجنب الـ Magic Numbers
```csharp
// ✗ سيء
if (speed > 5.5f && jumpHeight < 2.3f)
    // ...

// ✓ جيد
private const float MAX_SPEED = 5.5f;
private const float MIN_JUMP_HEIGHT = 2.3f;

if (speed > MAX_SPEED && jumpHeight < MIN_JUMP_HEIGHT)
    // ...
```

#### 5. استخدم Null Checking
```csharp
// ✓ جيد
if (health != null)
    health.TakeDamage(damage);
else
    Debug.LogWarning("Health component not found!");
```

---

## 3. استراتيجية الاستيراد (Importing Assets)

### استيراد النماذج

```csharp
// الإعدادات الموصى بها في Import Settings:
// 1. Model Tab
//    - Format: Imported Blend, Autodesk FBX, glTF
//    - Animation Type: Humanoid (للشخصيات)
//    - Avatar: Create From This Model

// 2. Rig Tab
//    - Animation Type: Humanoid
//    - Avatar: Create From This Model

// 3. Animation Tab
//    - Animation: على (Enabled)
//    - Bake Constraints: على
```

### استيراد الرسومات

```
Recommended Settings:
- Format: PNG (24-bit)
- Filter Mode: Bilinear
- Compression: Normal
- Max Size: 2048 أو 4096
- sRGB Color Space: على
```

### استيراد الأصوات

```
Music/BGM:
- Format: OGG (Vorbis)
- Compression: Vorbis
- Quality: 50-70
- Load Type: Streaming

SFX/Effects:
- Format: WAV
- Compression: PCM
- Load Type: Decompress On Load
```

---

## 4. نظام إدارة الموارد

### Object Pooling (لتحسين الأداء)

```csharp
public class ObjectPool<T> where T : MonoBehaviour
{
    private Queue<T> availableObjects = new Queue<T>();
    private T prefab;
    private Transform parent;
    
    public ObjectPool(T prefab, int initialSize, Transform parent = null)
    {
        this.prefab = prefab;
        this.parent = parent;
        
        for (int i = 0; i < initialSize; i++)
        {
            T obj = Instantiate(prefab, parent);
            obj.gameObject.SetActive(false);
            availableObjects.Enqueue(obj);
        }
    }
    
    public T GetObject()
    {
        if (availableObjects.Count > 0)
        {
            T obj = availableObjects.Dequeue();
            obj.gameObject.SetActive(true);
            return obj;
        }
        
        return Instantiate(prefab, parent);
    }
    
    public void ReturnObject(T obj)
    {
        obj.gameObject.SetActive(false);
        availableObjects.Enqueue(obj);
    }
}
```

### Resource Management
```csharp
// تحميل الموارد بشكل ديناميكي
public class AssetLoader
{
    public static T LoadAsset<T>(string path) where T : UnityEngine.Object
    {
        return Resources.Load<T>(path);
    }
    
    public static void LoadAssetAsync<T>(string path, System.Action<T> callback) 
        where T : UnityEngine.Object
    {
        ResourceRequest request = Resources.LoadAsync<T>(path);
        request.completed += op => callback((T)request.asset);
    }
}
```

---

## 5. نظام الحفظ والتحميل

### نموذج بسيط للحفظ

```csharp
[System.Serializable]
public class GameSaveData
{
    public Vector3 playerPosition;
    public float playerHealth;
    public InventoryData inventory;
    public Dictionary<string, int> completedPuzzles;
}

public class SaveManager : Singleton<SaveManager>
{
    private string savePath;
    
    private void Start()
    {
        savePath = Application.persistentDataPath + "/save.json";
    }
    
    public void SaveGame(GameSaveData data)
    {
        string json = JsonUtility.ToJson(data, true);
        System.IO.File.WriteAllText(savePath, json);
        Debug.Log("Game saved!");
    }
    
    public GameSaveData LoadGame()
    {
        if (!System.IO.File.Exists(savePath))
        {
            Debug.LogWarning("Save file not found!");
            return null;
        }
        
        string json = System.IO.File.ReadAllText(savePath);
        return JsonUtility.FromJson<GameSaveData>(json);
    }
}
```

---

## 6. نظام التصحيح (Debugging)

### أدوات التصحيح المفيدة

```csharp
public static class DebugHelper
{
    public static void DrawBounds(Bounds bounds, Color color, float duration = 0)
    {
        Vector3 center = bounds.center;
        Vector3 extents = bounds.extents;
        
        // رسم القاعدة
        Debug.DrawLine(
            center + new Vector3(-extents.x, -extents.y, -extents.z),
            center + new Vector3(extents.x, -extents.y, -extents.z),
            color, duration);
    }
    
    public static void LogPerformance(string label, System.Action action)
    {
        var watch = System.Diagnostics.Stopwatch.StartNew();
        action?.Invoke();
        watch.Stop();
        Debug.Log($"{label}: {watch.ElapsedMilliseconds}ms");
    }
}
```

### استخدام Conditional Compilation
```csharp
#if UNITY_EDITOR
    Debug.Log("This only runs in the editor");
#endif

#if DEVELOPMENT_BUILD || UNITY_EDITOR
    Debug.LogWarning("Performance issue detected!");
#endif
```

---

## 7. تحسينات الأداء

### نصائح مهمة

#### 1. استخدم Coroutines بدلاً من Loops
```csharp
// ✗ سيء - يوقف كل إطار
for (int i = 0; i < 1000; i++)
{
    CreateEnemy();
}

// ✓ جيد - ينتشر عبر عدة إطارات
StartCoroutine(SpawnEnemiesOverTime());

private IEnumerator SpawnEnemiesOverTime()
{
    for (int i = 0; i < 1000; i++)
    {
        CreateEnemy();
        if (i % 10 == 0)
            yield return null; // انتظر إطار واحد
    }
}
```

#### 2. استخدم Static Batching
```csharp
// في Inspector:
// قم بتعليم "Static" للأشياء التي لا تتحرك
```

#### 3. Optimize Colliders
```csharp
// استخدم بسيط Colliders بدلاً من Complex Mesh Colliders
// استخدم Rigidbody.isKinematic = true للأشياء الثابتة
```

#### 4. Use Object Pooling
```
بدلاً من Instantiate و Destroy باستمرار،
استخدم Object Pool لإعادة استخدام الكائنات
```

---

## 8. التوثيق والتعليقات

### نموذج توثيق جيد

```csharp
/// <summary>
/// يحسب الضرر بناءً على مسافة الانفجار
/// </summary>
/// <param name="explosionCenter">مركز الانفجار</param>
/// <param name="target">الهدف المتضرر</param>
/// <param name="baseDamage">الضرر الأساسي</param>
/// <returns>كمية الضرر النهائية</returns>
public static float CalculateExplosionDamage(
    Vector3 explosionCenter, 
    Transform target, 
    float baseDamage)
{
    float distance = Vector3.Distance(explosionCenter, target.position);
    float damageMultiplier = Mathf.Max(0, 1 - (distance / explosionRadius));
    return baseDamage * damageMultiplier;
}
```

---

## 9. الاختبار والـ QA

### قائمة اختبار أساسية لكل مرحلة

```markdown
## Phase Testing Checklist

### Gameplay
- [ ] اللاعب يستطيع التحرك بسلاسة
- [ ] القفز يعمل بشكل صحيح
- [ ] التفاعل مع الأشياء يعمل
- [ ] الكاميرا تتابع اللاعب بشكل صحيح

### Systems
- [ ] الصحة تنقص عند الضرر
- [ ] الأكسجين ينقص مع الوقت
- [ ] الجرد يقبل الموارد
- [ ] الحفظ والتحميل يعمل

### Performance
- [ ] FPS لا يقل عن 60
- [ ] لا توجد تسرب ذاكرة
- [ ] وقت التحميل معقول
- [ ] لا توجد أخطاء Console

### Quality
- [ ] النصوص صحيحة (بدون أخطاء إملائية)
- [ ] الأصوات مسموعة بوضوح
- [ ] الرسومات تبدو جيدة
- [ ] المشاهد تحمل بسلاسة
```

---

## 10. مصادر تعليمية مفيدة

### حول Unity
- [Unity Learn](https://learn.unity.com/)
- [Unity Documentation](https://docs.unity3d.com/)
- [Unity Forums](https://forum.unity.com/)

### حول البرمجة
- [Microsoft C# Documentation](https://docs.microsoft.com/en-us/dotnet/csharp/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/unity3d)

### حول تطوير الألعاب
- [Game Design Document Template](https://www.gamedeveloper.com/)
- [Gamasutra](https://www.gamasutra.com/) - مقالات الصناعة

### حول الفن والتصميم
- [Sketchfab](https://sketchfab.com/) - نماذج ثلاثية الأبعاد
- [Mixamo](https://www.mixamo.com/) - رسوم حركة
- [OpenGameArt](https://opengameart.org/) - موارد مجانية

---

## 11. جدول المشروع اليومي الموصى به

### كل يوم تطوير
```
09:00 - 09:30: المراجعة والتخطيط
09:30 - 12:00: العمل المركز
12:00 - 13:00: غداء
13:00 - 17:00: العمل المركز والاختبار
17:00 - 17:30: المراجعة والتوثيق
```

### أسبوعياً
```
يوم الاثنين: استعراض الأسبوع الماضي
الثلاثاء - الخميس: العمل المركز
الجمعة: الاختبار والمراجعة الشاملة
الأحد: التخطيط للأسبوع القادم (اختياري)
```

---

## 12. خدمات ومنصات مفيدة

### لإدارة المشروع
- [GitHub Projects](https://github.com/features/project-management)
- [Trello](https://trello.com/)
- [Asana](https://asana.com/)

### للتعاون
- [Discord](https://discord.com/) - للتواصل مع الفريق
- [GitHub](https://github.com/) - للتحكم بالنسخة

### للنشر والتوزيع
- [Steam](https://steampowered.com/) - PC Gaming
- [itch.io](https://itch.io/) - Independent Games
- [Epic Games Store](https://www.epicgames.com/store/)

---

## الخلاصة

هذا الدليل يوفر أساسيات قوية لبدء التطوير. تذكر:

1. **الجودة أولاً** - لا تسرع على حساب الجودة
2. **الاختبار المستمر** - اختبر كل ميزة قبل المتابعة
3. **التوثيق** - وثق عملك لمساعدة نفسك والآخرين لاحقاً
4. **المرونة** - كن مستعداً للتعديل على الخطة
5. **الاستمتاع** - استمتع بالعملية الإبداعية!

---

**آخر تحديث**: 17 سبتمبر 2026
**الحالة**: نسخة أولى متكاملة
