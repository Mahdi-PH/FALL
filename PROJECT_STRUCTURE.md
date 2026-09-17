# 📁 هيكل المشروع والملفات البرمجية الأساسية

## 1. هيكل مجلدات المشروع

```
FALL/
├── Assets/                          # جميع موارد اللعبة
│   │
│   ├── Models/                      # النماذج ثلاثية الأبعاد
│   │   ├── Characters/
│   │   │   ├── Player/
│   │   │   │   └── player_model.fbx
│   │   │   └── Helmets/
│   │   ├── Enemies/
│   │   │   ├── Enemy_Type1/
│   │   │   ├── Enemy_Type2/
│   │   │   └── Enemy_Boss/
│   │   └── Props/
│   │       ├── Doors/
│   │       ├── Containers/
│   │       ├── Structures/
│   │       └── Decorations/
│   │
│   ├── Textures/                    # الصور والألوان
│   │   ├── Characters/
│   │   ├── Environments/
│   │   ├── Props/
│   │   └── UI/
│   │
│   ├── Animations/                  # رسوم الحركة
│   │   ├── Player/
│   │   │   ├── Movement/
│   │   │   ├── Interaction/
│   │   │   └── Combat/
│   │   └── Enemies/
│   │       ├── Enemy_Type1/
│   │       ├── Enemy_Type2/
│   │       └── Enemy_Boss/
│   │
│   ├── Audio/                       # الأصوات والموسيقى
│   │   ├── Music/
│   │   │   ├── Exploration.ogg
│   │   │   ├── Combat.ogg
│   │   │   ├── Caves.ogg
│   │   │   └── Ruins.ogg
│   │   └── SFX/
│   │       ├── Player/
│   │       ├── Enemies/
│   │       ├── Environment/
│   │       └── UI/
│   │
│   ├── Materials/                   # مواد الرسومات
│   │   ├── Characters/
│   │   ├── Environments/
│   │   └── Props/
│   │
│   ├── Prefabs/                     # النماذج المعدة مسبقاً
│   │   ├── Characters/
│   │   │   └── Player.prefab
│   │   ├── Enemies/
│   │   │   ├── Enemy_Type1.prefab
│   │   │   ├── Enemy_Type2.prefab
│   │   │   └── Enemy_Boss.prefab
│   │   ├── Props/
│   │   │   ├── Door.prefab
│   │   │   ├── Container.prefab
│   │   │   └── Platform.prefab
│   │   └── UI/
│   │       ├── MainCanvas.prefab
│   │       ├── HUD.prefab
│   │       └── Menu.prefab
│   │
│   ├── Scenes/                      # مشاهد اللعبة
│   │   ├── MainMenu.unity
│   │   ├── Level_1_CrashSite.unity
│   │   ├── Level_2_Caves.unity
│   │   ├── Level_3_Ruins.unity
│   │   ├── Level_4_Desert.unity
│   │   └── Pause.unity
│   │
│   ├── Scripts/                     # جميع الأكواد البرمجية
│   │   ├── Core/                    # الأنظمة الأساسية
│   │   │   ├── GameManager.cs
│   │   │   ├── SceneManager.cs
│   │   │   ├── EventSystem.cs
│   │   │   └── InputHandler.cs
│   │   │
│   │   ├── Player/                  # نظام اللاعب
│   │   │   ├── PlayerController.cs
│   │   │   ├── PlayerHealth.cs
│   │   │   ├── PlayerMovement.cs
│   │   │   ├── PlayerAnimation.cs
│   │   │   └── Equipment.cs
│   │   │
│   │   ├── Systems/                 # الأنظمة المختلفة
│   │   │   ├── HealthSystem.cs
│   │   │   ├── ResourceManager.cs
│   │   │   ├── InventorySystem.cs
│   │   │   ├── CraftingSystem.cs
│   │   │   ├── SaveSystem.cs
│   │   │   └── CameraController.cs
│   │   │
│   │   ├── Enemy/                   # نظام الأعداء
│   │   │   ├── EnemyController.cs
│   │   │   ├── AIBehavior.cs
│   │   │   ├── EnemyHealth.cs
│   │   │   ├── PatrolState.cs
│   │   │   ├── ChaseState.cs
│   │   │   └── AttackState.cs
│   │   │
│   │   ├── Interaction/             # التفاعل والألغاز
│   │   │   ├── Interactable.cs
│   │   │   ├── Door.cs
│   │   │   ├── Container.cs
│   │   │   ├── Terminal.cs
│   │   │   └── PuzzleController.cs
│   │   │
│   │   ├── Combat/                  # نظام القتال
│   │   │   ├── CombatSystem.cs
│   │   │   ├── Weapon.cs
│   │   │   ├── ProjectileBase.cs
│   │   │   └── DamageDealer.cs
│   │   │
│   │   ├── UI/                      # الواجهة الرسومية
│   │   │   ├── UIManager.cs
│   │   │   ├── HUDController.cs
│   │   │   ├── MenuController.cs
│   │   │   ├── InventoryUI.cs
│   │   │   └── DialogueUI.cs
│   │   │
│   │   ├── Environment/             # البيئة والخريطة
│   │   │   ├── EnvironmentManager.cs
│   │   │   ├── LevelTrigger.cs
│   │   │   ├── MapGenerator.cs
│   │   │   └── ClimateSystem.cs
│   │   │
│   │   └── Utils/                   # الأدوات المساعدة
│   │       ├── ObjectPool.cs
│   │       ├── Singleton.cs
│   │       ├── Extensions.cs
│   │       ├── Constants.cs
│   │       └── Logger.cs
│   │
│   ├── Resources/                   # الموارد اللازمة في الوقت التشغيلي
│   │   ├── Config/
│   │   │   ├── GameConfig.json
│   │   │   ├── LevelConfig.json
│   │   │   └── EnemyConfig.json
│   │   └── Data/
│   │       ├── PlayerData.json
│   │       └── SaveData/
│   │
│   └── Editor/                      # أدوات المحرر المخصصة
│       ├── CustomInspectors/
│       └── EditorWindows/
│
├── ProjectSettings/                 # إعدادات Unity
│   ├── ProjectVersion.txt
│   ├── AudioManager.asset
│   ├── GraphicsSettings.asset
│   ├── InputManager.asset
│   ├── QualitySettings.asset
│   └── TagManager.asset
│
├── Packages/                        # حزم Unity
│   ├── manifest.json
│   └── packages-lock.json
│
├── Documentation/                   # ملفات التوثيق
│   ├── GameDesignDoc.md
│   ├── TechnicalSpec.md
│   ├── API_Reference.md
│   ├── SYSTEMS_GUIDE.md
│   └── ARCHITECTURE.md
│
├── README.md                        # الملف الرئيسي
├── ASSETS_CHECKLIST.md              # قائمة الـ Assets
├── PROJECT_STRUCTURE.md             # هذا الملف
├── .gitignore
└── .gitattributes
```

---

## 2. الملفات البرمجية الأساسية الموصى بها

### Core/GameManager.cs
```csharp
public class GameManager : Singleton<GameManager>
{
    [SerializeField] private GameState currentState;
    [SerializeField] private float gameSeed;
    
    private Dictionary<string, System.Object> systems = new();
    
    public event System.Action OnGameStart;
    public event System.Action OnGamePause;
    public event System.Action OnGameResume;
    public event System.Action OnGameEnd;
    
    protected override void Awake()
    {
        base.Awake();
        InitializeSystems();
    }
    
    private void InitializeSystems()
    {
        // تهيئة جميع أنظمة اللعبة
    }
    
    public T GetSystem<T>(string systemName) where T : class
    {
        return systems.ContainsKey(systemName) ? 
            systems[systemName] as T : null;
    }
    
    public void PauseGame() { /* ... */ }
    public void ResumeGame() { /* ... */ }
    public void EndGame() { /* ... */ }
}
```

### Player/PlayerController.cs
```csharp
public class PlayerController : MonoBehaviour
{
    [SerializeField] private PlayerMovement movement;
    [SerializeField] private PlayerHealth health;
    [SerializeField] private InventorySystem inventory;
    
    private InputHandler input;
    private Animator animator;
    
    private void Start()
    {
        input = InputHandler.Instance;
        animator = GetComponent<Animator>();
    }
    
    private void Update()
    {
        HandleInput();
        UpdateAnimation();
    }
    
    private void HandleInput()
    {
        // معالجة الإدخال من الكيبورد/جويستيك
    }
    
    public void TakeDamage(float damage)
    {
        health.ReduceHealth(damage);
    }
}
```

### Systems/HealthSystem.cs
```csharp
public class HealthSystem : MonoBehaviour
{
    [SerializeField] private float maxHealth = 100f;
    [SerializeField] private float regenerationRate = 0.5f;
    
    private float currentHealth;
    
    public event System.Action<float> OnHealthChanged;
    public event System.Action OnDeath;
    
    private void Start()
    {
        currentHealth = maxHealth;
    }
    
    public void TakeDamage(float damage)
    {
        currentHealth = Mathf.Max(0, currentHealth - damage);
        OnHealthChanged?.Invoke(currentHealth);
        
        if (currentHealth <= 0)
            OnDeath?.Invoke();
    }
    
    public void Heal(float amount)
    {
        currentHealth = Mathf.Min(maxHealth, currentHealth + amount);
        OnHealthChanged?.Invoke(currentHealth);
    }
    
    public float GetHealthPercentage() => currentHealth / maxHealth;
}
```

### Systems/InventorySystem.cs
```csharp
public class InventorySystem : MonoBehaviour
{
    [SerializeField] private int maxSlots = 20;
    [SerializeField] private float maxWeight = 50f;
    
    private List<InventoryItem> items = new();
    private float currentWeight = 0f;
    
    public event System.Action OnInventoryChanged;
    
    public bool AddItem(InventoryItem item)
    {
        if (currentWeight + item.weight > maxWeight)
            return false;
            
        items.Add(item);
        currentWeight += item.weight;
        OnInventoryChanged?.Invoke();
        return true;
    }
    
    public bool RemoveItem(InventoryItem item)
    {
        bool result = items.Remove(item);
        if (result)
        {
            currentWeight -= item.weight;
            OnInventoryChanged?.Invoke();
        }
        return result;
    }
    
    public List<InventoryItem> GetAllItems() => new List<InventoryItem>(items);
}
```

### Enemy/EnemyController.cs
```csharp
public class EnemyController : MonoBehaviour
{
    [SerializeField] private float speed = 3.5f;
    [SerializeField] private float detectionRange = 10f;
    [SerializeField] private float attackRange = 2f;
    
    private EnemyHealth health;
    private NavMeshAgent agent;
    private StateMachine stateMachine;
    
    private void Start()
    {
        health = GetComponent<EnemyHealth>();
        agent = GetComponent<NavMeshAgent>();
        InitializeStateMachine();
    }
    
    private void InitializeStateMachine()
    {
        stateMachine = new StateMachine();
        stateMachine.AddState("Patrol", new PatrolState(this));
        stateMachine.AddState("Chase", new ChaseState(this));
        stateMachine.AddState("Attack", new AttackState(this));
    }
    
    public void DetectPlayer(Transform playerTransform)
    {
        float distance = Vector3.Distance(transform.position, playerTransform.position);
        if (distance <= detectionRange)
            stateMachine.SetState("Chase");
    }
}
```

### UI/HUDController.cs
```csharp
public class HUDController : MonoBehaviour
{
    [SerializeField] private Image healthBar;
    [SerializeField] private Image oxygenBar;
    [SerializeField] private Text healthText;
    [SerializeField] private Text oxygenText;
    
    private PlayerHealth playerHealth;
    private OxygenSystem oxygenSystem;
    
    private void Start()
    {
        playerHealth = FindObjectOfType<PlayerHealth>();
        oxygenSystem = FindObjectOfType<OxygenSystem>();
        
        playerHealth.OnHealthChanged += UpdateHealthBar;
        oxygenSystem.OnOxygenChanged += UpdateOxygenBar;
    }
    
    private void UpdateHealthBar(float health, float maxHealth)
    {
        healthBar.fillAmount = health / maxHealth;
        healthText.text = $"{health:F0} / {maxHealth:F0}";
    }
    
    private void UpdateOxygenBar(float oxygen, float maxOxygen)
    {
        oxygenBar.fillAmount = oxygen / maxOxygen;
        oxygenText.text = $"{oxygen:F0} / {maxOxygen:F0}";
    }
}
```

### Utils/Singleton.cs
```csharp
public abstract class Singleton<T> : MonoBehaviour where T : Singleton<T>
{
    public static T Instance { get; private set; }
    
    protected virtual void Awake()
    {
        if (Instance != null && Instance != this)
        {
            Destroy(gameObject);
            return;
        }
        
        Instance = (T)Convert.ChangeType(this, typeof(T));
        DontDestroyOnLoad(gameObject);
    }
    
    protected virtual void OnDestroy()
    {
        if (Instance == this)
            Instance = null;
    }
}
```

---

## 3. Tags والطبقات المطلوبة

### Tags
```
Player
Enemy
Interactable
Projectile
Collectible
Hazard
Door
Platform
```

### Layers
```
0:  Default
1:  TransparentFX
2:  Ignore Raycast
3:  (فارغ)
4:  Water
5:  UI
6:  Player
7:  Enemy
8:  Interactive
9:  Projectile
10: Collectible
```

---

## 4. الحزم والمكتبات المقترحة

### Unity Built-in
- TextMesh Pro
- Timeline
- Cinemachine
- Animator
- Physics Engine
- Audio Engine

### من Unity Asset Store
- DOTween (للرسوم المتقدمة)
- Odin Inspector (لتحسين الـ Inspector)
- PlayMaker (للـ Visual Scripting - اختياري)

---

## 5. معايير الملفات والتسمية

### ملفات السكريبت
- **PascalCase** للأسماء: `PlayerController.cs`
- **كلاسات**: تبدأ بـ Capital letter
- **متغيرات خاصة**: بادئة underscore: `_health`
- **متغيرات عامة**: PascalCase

### ملفات الموارد
- **المشاهد**: Level_1_Name.unity
- **الـ Prefabs**: PrefabName.prefab
- **المواد**: MAT_Name.mat
- **الرسومات**: TEX_Name.png

### تسمية الأشياء في المشهد
```
[TYPE]_Name
[CHAR]_Player
[ENEMY]_Type1
[PROP]_Door
[LIGHT]_Sun
[AUDIO]_BGM
```

---

## 6. الإعدادات الموصى بها

### جودة الرسومات
- **الدقة**: 1920x1080 (حد أدنى)
- **FPS المستهدف**: 60+
- **Shadow Quality**: Medium
- **Texture Quality**: Medium/High

### صيغ الحفظ
- **النماذج**: FBX
- **الرسومات**: PNG (بخلفية شفافة)
- **الموسيقى**: OGG
- **مؤثرات صوتية**: WAV

---

**آخر تحديث**: 17 سبتمبر 2026
**الحالة**: نسخة أولى متكاملة
