# 🗺️ خريطة الطريق (Roadmap)

## نظرة عامة سريعة

```
Week 1-4       Week 5-8       Week 9-12      Week 13-16     Week 17-20     Week 21-24
├─ Setup       ├─ Survival    ├─ Puzzles    ├─ Combat      ├─ Content    ├─ Testing
├─ Basics      ├─ Resources   ├─ Props      ├─ AI          ├─ Level 4    ├─ Polish
└─ Level 1     └─ Inventory   └─ Level 2-3  └─ Enemies     └─ Music      └─ Launch
```

---

## المرحلة 1: الأساسيات (الأسابيع 1-4)

### الأسبوع 1: الإعداد والتخطيط

#### الأهداف الرئيسية
- [ ] إنشاء مشروع Unity جديد
- [ ] استيراد الـ Assets الأساسية
- [ ] إعداد هيكل المشروع
- [ ] تنظيم نظام التحكم بالنسخة (Git)

#### المهام التفصيلية
```csharp
// إنشاء المشروع
- إنشاء مشروع Unity 2022 LTS
- تعريب الإعدادات إذا لزم الأمر
- تثبيت المكونات المطلوبة

// استيراد الأساسيات
- استيراد نموذج الشخصية
- استيراد رسوم الحركة الأساسية
- استيراد أول مجموعة نصوص
- استيراد أول مجموعة رسومات

// هيكل المشروع
- إنشاء المجلدات حسب الخطة
- إعداد Tags و Layers
- إعداد Project Settings الأساسية
```

#### المخرجات المتوقعة
- ✓ مشروع نظيف وجاهز
- ✓ الـ Assets مستوردة بشكل صحيح
- ✓ Git مهيأ وجاهز للاستخدام

---

### الأسبوع 2: نظام التحكم الأساسي

#### الأهداف الرئيسية
- [ ] تطوير PlayerController
- [ ] نظام الإدخال (Input Handler)
- [ ] كاميرا تابعة

#### المهام التفصيلية
```csharp
// PlayerController
- حركة اللاعب (WASD)
- القفز
- رسوم الحركة الأساسية
- تصادمات جسم اللاعب

// Input Handler
- قراءة مدخلات الكيبورد
- قراءة مدخلات الجويستيك
- إعادة تعيين المفاتيح

// Cinemachine Camera
- كاميرا تتبع اللاعب
- تحكم بالعرض (بواسطة الماوس)
- حدود الكاميرا
```

#### الكود الأساسي
```csharp
public class PlayerController : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;
    [SerializeField] private float jumpForce = 5f;
    
    private Rigidbody rb;
    private Animator animator;
    private float verticalInput;
    private float horizontalInput;
    
    private void Start()
    {
        rb = GetComponent<Rigidbody>();
        animator = GetComponent<Animator>();
    }
    
    private void Update()
    {
        HandleInput();
        UpdateAnimation();
    }
    
    private void FixedUpdate()
    {
        Move();
    }
    
    private void HandleInput()
    {
        horizontalInput = Input.GetAxis("Horizontal");
        verticalInput = Input.GetAxis("Vertical");
        
        if (Input.GetKeyDown(KeyCode.Space))
            Jump();
    }
    
    private void Move()
    {
        Vector3 moveDirection = new Vector3(horizontalInput, 0, verticalInput).normalized;
        rb.velocity = moveDirection * moveSpeed + 
                      new Vector3(0, rb.velocity.y, 0);
    }
    
    private void Jump()
    {
        rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
    }
    
    private void UpdateAnimation()
    {
        float speed = new Vector3(rb.velocity.x, 0, rb.velocity.z).magnitude;
        animator.SetFloat("Speed", speed);
    }
}
```

#### المخرجات المتوقعة
- ✓ اللاعب يتحرك بسلاسة
- ✓ القفز يعمل بشكل صحيح
- ✓ الرسوم الحركية تتغير تلقائياً
- ✓ الكاميرا تتابع اللاعب

---

### الأسبوع 3: المشهد الأول (Level 1)

#### الأهداف الرئيسية
- [ ] بناء أول مستوى
- [ ] استيراد Props والبيئة
- [ ] إعدادات الضوء والسماء

#### المهام التفصيلية
- بناء تضاريس موقع الحطام
- استيراد أنقاض المركبة
- وضع الحجارة والموارد
- إضاءة الإضاءات الديناميكية
- سماء وتأثيرات جوية

#### المخرجات المتوقعة
- ✓ مستوى أول قابل للاستكشاف
- ✓ بيئة بصرية جذابة
- ✓ أداء جيدة (60+ FPS)

---

### الأسبوع 4: المراجعة والتحسينات

#### المهام
- [ ] اختبار شامل للمرحلة الأولى
- [ ] إصلاح الأخطاء
- [ ] تحسينات الأداء
- [ ] توثيق الأنظمة

#### معايير القبول
- ✓ بدون أخطاء حرجة
- ✓ أداء 60+ FPS
- ✓ تجربة لعب سلسة

---

## المرحلة 2: أنظمة البقاء (الأسابيع 5-8)

### الأسبوع 5: نظام الصحة والأكسجين

```csharp
// Health System
public class HealthSystem : MonoBehaviour
{
    [SerializeField] private float maxHealth = 100f;
    private float currentHealth;
    
    public event System.Action<float, float> OnHealthChanged;
    
    private void Start() => currentHealth = maxHealth;
    
    public void TakeDamage(float damage)
    {
        currentHealth = Mathf.Max(0, currentHealth - damage);
        OnHealthChanged?.Invoke(currentHealth, maxHealth);
    }
    
    public void Heal(float amount)
    {
        currentHealth = Mathf.Min(maxHealth, currentHealth + amount);
        OnHealthChanged?.Invoke(currentHealth, maxHealth);
    }
}

// Oxygen System
public class OxygenSystem : MonoBehaviour
{
    [SerializeField] private float maxOxygen = 100f;
    [SerializeField] private float depletionRate = 5f;
    
    private float currentOxygen;
    public event System.Action<float, float> OnOxygenChanged;
    
    private void Start() => currentOxygen = maxOxygen;
    
    private void Update()
    {
        currentOxygen = Mathf.Max(0, currentOxygen - depletionRate * Time.deltaTime);
        OnOxygenChanged?.Invoke(currentOxygen, maxOxygen);
    }
}
```

### الأسبوع 6: نظام الموارد والجرد

```csharp
[System.Serializable]
public class InventoryItem
{
    public string id;
    public string name;
    public float weight;
    public Sprite icon;
}

public class InventorySystem : MonoBehaviour
{
    [SerializeField] private int maxSlots = 20;
    [SerializeField] private float maxWeight = 50f;
    
    private List<InventoryItem> items = new();
    private float currentWeight = 0f;
    
    public event System.Action OnInventoryChanged;
    
    public bool AddItem(InventoryItem item)
    {
        if (currentWeight + item.weight > maxWeight) return false;
        
        items.Add(item);
        currentWeight += item.weight;
        OnInventoryChanged?.Invoke();
        return true;
    }
}
```

### الأسابيع 7-8: HUD والحفظ

- تطوير HUD لعرض الصحة والأكسجين
- نظام حفظ وتحميل أساسي
- اختبار شامل للأنظمة

---

## المرحلة 3: التفاعل والألغاز (الأسابيع 9-12)

### الأسبوع 9: نظام التفاعل الأساسي

```csharp
public class Interactable : MonoBehaviour
{
    public virtual void Interact(PlayerController player)
    {
        Debug.Log("Interacted with " + gameObject.name);
    }
}

public class Door : Interactable
{
    [SerializeField] private bool isLocked = false;
    [SerializeField] private Animator animator;
    
    public override void Interact(PlayerController player)
    {
        if (isLocked)
        {
            Debug.Log("Door is locked!");
            return;
        }
        
        animator.SetTrigger("Open");
    }
}
```

### الأسابيع 10-11: الألغاز البيئية

- لغز مفاتيح الأبواب
- لغز تفعيل الأجهزة
- لغز تحريك الأجسام

### الأسبوع 12: المنطقة الثانية

- بناء الكهوف المضيئة
- استيراد البلورات والنبتات الغريبة
- ربط المنطقتين

---

## المرحلة 4: القتال والأعداء (الأسابيع 13-16)

### الأسابيع 13-14: نظام AI الأساسي

```csharp
public class EnemyController : MonoBehaviour
{
    [SerializeField] private float detectionRange = 10f;
    [SerializeField] private float attackRange = 2f;
    
    private StateMachine stateMachine;
    private Transform playerTransform;
    
    private void Start()
    {
        stateMachine = new StateMachine();
        InitializeStates();
        playerTransform = FindObjectOfType<PlayerController>().transform;
    }
    
    private void Update()
    {
        CheckPlayerDetection();
    }
    
    private void CheckPlayerDetection()
    {
        float distance = Vector3.Distance(transform.position, playerTransform.position);
        
        if (distance < detectionRange)
            stateMachine.SetState("Chase");
        else
            stateMachine.SetState("Patrol");
    }
    
    private void InitializeStates()
    {
        stateMachine.AddState("Patrol", new PatrolState(this));
        stateMachine.AddState("Chase", new ChaseState(this, playerTransform));
        stateMachine.AddState("Attack", new AttackState(this, playerTransform));
    }
}
```

### الأسابيع 15-16: القتال والمعارك

- نظام السلاح والأضرار
- أنواع أعداء مختلفة
- معارك اختبارية

---

## المرحلة 5: المحتوى والتلميع (الأسابيع 17-20)

### الأسابيع 17-18: المستويات الإضافية

- بناء أطلال المدينة (Level 3)
- بناء الصحراء الشاسعة (Level 4)
- ربط المستويات

### الأسابيع 19-20: الموسيقى والمؤثرات

- إضافة موسيقى الخلفية
- إضافة مؤثرات صوتية
- إضافة أصوات التفاعلات

---

## المرحلة 6: الاختبار والتحسين (الأسابيع 21-24)

### الأسبوع 21: QA Testing

```
□ اختبار جميع المستويات
□ اختبار جميع الأنظمة
□ اختبار الحفظ والتحميل
□ اختبار الأداء
□ اختبار توافق الأجهزة المختلفة
```

### الأسبوع 22: إصلاح الأخطاء

- تجميع كل الأخطاء المكتشفة
- أولويات الإصلاح
- الاختبار المتكرر

### الأسبوع 23: الموازنة والتحسين

- موازنة صعوبة اللعبة
- تحسينات الأداء النهائية
- تحسينات الرسومات

### الأسبوع 24: الإطلاق

- البناء النهائي
- الاختبار النهائي
- الإطلاق! 🚀

---

## نقاط تحقق أساسية

### نهاية المرحلة 1
- ✓ مشروع عامل بدون أخطاء
- ✓ نظام تحكم سلس
- ✓ مستوى أول جميل

### نهاية المرحلة 2
- ✓ أنظمة بقاء متكاملة
- ✓ HUD يعمل بشكل صحيح
- ✓ حفظ وتحميل يعمل

### نهاية المرحلة 3
- ✓ تفاعلات ممتعة
- ✓ ألغاز شيقة
- ✓ منطقتان متصلتان

### نهاية المرحلة 4
- ✓ قتال ممتع
- ✓ أعداء ذكيين
- ✓ معارك متوازنة

### نهاية المرحلة 5
- ✓ 4 مستويات جميلة
- ✓ موسيقى وصوت احترافي
- ✓ لعبة متكاملة

### نهاية المرحلة 6
- ✓ لعبة خالية من الأخطاء الحرجة
- ✓ أداء عالية
- ✓ جاهزة للإطلاق

---

## ملاحظات مهمة

### المرونة
- هذه الخطة مرنة ويمكن تعديلها
- إذا تأخرت مرحلة ما، قد تحتاج لتقليل النطاق

### الأولويات
1. الجودة أولاً
2. الأداء ثانياً
3. السرعة ثالثاً

### الاختبار المستمر
- اختبر كل ميزة في نفس الأسبوع
- لا تجمع الاختبار في النهاية

### التوثيق المستمر
- وثق الأنظمة الجديدة فوراً
- احفظ النوتات والأفكار

---

**آخر تحديث**: 17 سبتمبر 2026
**الحالة**: خطة تفصيلية شاملة
