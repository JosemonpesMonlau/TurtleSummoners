<h1>Turtle Summoners</h1>

Dentro de este documento se detalla el proyecto que incluye el juego gacha Turtle Summoners, basado en distintos juegos populares como 7ds y Pokemon, para el proyecto final de 2 DAM. Se describirá el sistema de carpetas de este repositorio, cómo jugar a la versión final del juego y el código del proyecto realizado.

<h1>1. Sistema de carpetas del repositorio</h1>

<h2>1.1 Project</h2> 
Carpeta en la que se encuentra el proyecto desarrollado en la versión Unity 2021.3.19f1. Dentro de la misma, se podrá encontrar la carpeta Assets, en cuyo interior podremos encontrar las siguientes subcarpetas:

1. **Prefabs:** Plantillas a partir de la cual se pueden crear nuevas instancias del objeto en la escena
2. **Resources:** Imágenes para los fondos de las diferentes pantallas asi como otros objetos esteticos y localicación de los archivos JSON
3. **Scenes:** Carpeta donde se almacenan las escenas del juego. En ella encontraremos 17: CombatSystem, para los combates de la historia, son 2vs2; CombatBoss1, CombatBoss2 y CombatBoss3, donde se desarrolla el combate contra enemigos fuertes; PantallaAjustes, donde se elegiria los ajustes de la app; PantallaBosses, donde se escogerá contra que jefe pelear; PantallaEleccion1 y PantallaEleccion2, en la primera se escogeran los personajes que usaras en las batallas de la historia y  en la segunda se escogeran los personajes que usaras en las batallas contra jefes; PantallaGacha, donde se podrán conseguir los personajes y se asignarán al usuario; PantallaHistoria, donde se selecciona que parte de la historia quieres jugar; PantallaInicio, primera pantalla, donde accedemos al juego; PantallaInventario, donde podrías ver tus objetos; PantallaMenu, donde accedemos a todas las pantallas principales; PantallaMisiones, donde se accederia a las misiones hechas y por hacer; PantallaPerfil, donde podrías ver tu información de usuario; PantallaPJs, donde puedes ver tu lista de personajes; PantallaTienda, donde podrías adquirir recursos del juego.
4. **Scripts:** Los diferentes scripts que se han desarrollado con la lógica del juego: En la carpeta ChangeScenes tenemos ChangeScene.cs, ChangeSceneHistoria.cs y ChangeSceneBoss.cs. En la carpeta ChooseCharacter tenemos Characters.cs y ShowCharacter.cs. En la carpeta Combat tenemos CombatManager.cs y Team.cs. En la carpeta Fighters tenemos EnemyFighter.cs, Fighter.cs, PlayerFighter.cs y Stats.cs. En la carpeta Gacha tenemos Gacha.cs y popUpgacha.cs. En la carpeta Header tenemos header.cs. En la carpeta Skills tenemos HealthModSkill.cs, Skill.cs, SkillTargeting.cs, StatusMod.cs y StatusModSkill.cs. En la carpeta StatusCondition tenemos ApplySCSkill.cs, HealthModStatusCondition.cs, StatusCondition.cs y TurnBlockStatusCondition.cs. En la carpeta UI tenemos EnemiesPanel.cs, EnemyButtonUI.cs, LogPanel.cs, PlayerSkillPanel.cs, StatusPanel.cs y Volver.cs. Se entrará más en detalle de los mismos en la parte de este readme donde se detalla el código.
5. **Sprites:** Los sprites que se han desarrollado para el juego.
6. **TextMesh Pro:** Proporciona un control mejorado sobre el formato y el diseño del texto con características como espaciado entre caracteres, palabras, líneas y párrafos, etc.
7. **Unity.VisualScripting.Generated:** Es una forma gráfica de manipular los objetos y los comportamientos en Unity sin tener que escribir código desde cero. La lógica se construye conectando nodos visuales, lo que permite que artistas, diseñadores y programadores creen juegos y sistemas interactivos con facilidad.

<h1>2. Ejecución del proyecto</h1>
Para la ejecución del proyecto necesitamos entrar en Unity y seleccionar la PantallaInicio que está ubicada en la carpeta assets/Scenes. Cuando este en la PantallaInicio darle al boton play en la parte superior de la pantalla.

En su defecto, ejecutar la apk disponible.

<h1>3. Detalle del desarrollo realizado</h1>
<h2>3.1 PantallaInicio</h2>
La pantalla inicial del juego es la de PantallaInicio. Ésta está construida a través de un canvas, una imagen como fondo y un boton invisible que al pulsarlo realiza esta acción:

1. **Botón Entrada:** Al pulsarlo, llama al método Volver del script ChangeScene. Lo único que realiza este método es cargar la escena del menú principal, llamada PantallaMenu, a través del SceneManager.LoadScene("Scenes/PantallaManu");

<h2>3.2 PantallaMenu</h2>
La pantalla de PantallaMenu, donde se desarrolla el menú para acceder a las distintas pantallas, se ha desarrollado a través de un canvas, un objeto de imagen para la imagen de fondo del juego, un Gameobject vacío donde se agrupan los componentes que forman el banner donde salen los datos del usuario, un Boton Ajustes que nos llevara a la PanatallaAjustes para modificar los ajustes del juego, un Panel donde agrupamos los botones para ir a la PantallaHistoria, PantallaBosses, y PantallaPJs, otro Panel para agrupar los botones que nos llevarán a PantallaGacha, PantallaTienda y PantallaInventario y como último un botón Profile que nos lleva a la PantallaPerfil.

<h2>3.2.1 El script ChangeScene.cs</h2>
En este fichero cs se encuentra la función Volver() que se le pasa al OnClick() de los botones necesarios. Un ejemplo de su estructura sería el siguiente:

```csharp
public class ChangeScene : MonoBehaviour
{
    public void Volver(string pantallas)
    {
        SceneManager.LoadScene("Scenes/"+pantallas);
    }
}
```

<h2>3.2.2 El script usuarios.json</h2>
En este fichero json se encuentran almacenados los datos de los usuarios. Un ejemplo de su estructura sería el siguiente:

```json
{
    "usuario": "juan",
    "email": "juan@monlau.com",
    "password": "12345678Monlau",
    "nivel": "20",
    "monedas": "1000",
    "gemas": "30",
    "personajes": [
        {
            "name": "Torti",
            "type": "cyan",
            "lore": "",
            "lvl": 99,
            "stats": {
                "hp": 9000,
                "defense": 50000,
                "atk": 40000,
                "speed": 330
            },
            "Skills": {
                "passive": {
                    "id_skills": 0,
                    "type_skill": "",
                    "name": "Un buen ataque es una buena defensa",
                    "description": "Las habilidades de daños escalan con defensa un 30%"
                },
                "skill1": {
                    "id_skills": 0,
                    "type_skill": "",
                    "name": "Estallido de cáscara",
                    "description": "Aumenta la defensa en 20%"
                },
                "skill2": {
                    "id_skills": 0,
                    "type_skill": "",
                    "name": "Puño escama",
                    "description": "Golpea repetidamente con sus feroces puños"
                },
                "Ulti": {
                    "id_skills": 0,
                    "type_skill": "",
                    "name": "rest",
                    "description": "Cura toda la vida"
                }
            }
        },
    ]
}
```

<h2>3.2.3 El script header.cs</h2>
En este fichero cs se recogen los datos de usuarios.json. Un ejemplo de su estructura sería el siguiente:
<!-- CUANDO SE ARREGLE -->


<h2>3.3 PantallaHistoria</h2>
La pantalla de PantallaHistoria, es donde se desarrolla el menú para acceder a las distintas batallas de la propia historia, se ha desarrollado a través de un canvas, un objeto de imagen para la imagen de fondo del juego, un Gameobject vacío donde se agrupan los componentes que forman el banner donde salen los datos del usuario, un Boton Volver que nos llevara de vuelta a la PanatallaMenu, y como último un GameObject vacio donde agrupamos los botones para ir a la PantallaEleccion1 pasandole un ID para acceder a los distintos niveles de la historia.

<h2>3.3.1 El script ChangeSceneHistoria.cs</h2>
En este fichero cs se encuentra la función ChangeScene() que se le pasa al OnClick() de los botones necesarios. Pasará un ID a la siguiente pantalla para identificar a que batalla acceder. Un ejemplo de su estructura sería el siguiente:

```csharp
public class ChangeSceneHistoria : MonoBehaviour
{
    public int id;
    public void ChangeScene(string pantallas)
    {
        SceneManager.LoadScene("Scenes/"+pantallas);
        PlayerPrefs.SetInt("ID", id);
    }
}
```

<h2>3.3.2 El script BotonVolver.cs</h2>
En este fichero cs se encuentra la función StartNewGame() que se le pasa al OnClick() del boton Volver. Un ejemplo de su estructura sería el siguiente:

```csharp
public class BotonVolver : MonoBehaviour
{
    public void StartNewGame() { SceneManager.LoadScene("Scenes/PantallaMenu"); }
}
```


<h2>3.4 PantallaEleccion1</h2>
La pantalla de PantallaEleccion1, es donde se desarrolla el menú para escoger los personajes y acceder a la batalla seleccionada de la historia, se ha desarrollado a través de un canvas, un Gameobject vacío donde se agrupan los componentes que forman el banner donde salen los datos del usuario, un Panel donde se visualizarian los personajes, un GameObject vacio donde se agrupan 2 filtros de personajes para escoger, un Boton Volver que nos llevara de vuelta a la PanatallaHistoria, y como último un Boton Start para ir a la pantalla CombatSystem que es la pantalla de 2vs2, pasandole el ID anterior para que se modifique la dificultad.

<h2>3.4.1 El script Characters.cs</h2>
En este fichero cs se encuentra las funciones Start(), Update() y OnDropdownValueChanged(). Recoge los datos del JSON para insertarlos en los desplegables. Un ejemplo de su estructura sería el siguiente:

```csharp
public class Characters : MonoBehaviour
{
    public TMP_Dropdown dropdownPJ1;
    public TMP_Dropdown dropdownPJ2;
    public TextAsset usuarios;


    [System.Serializable]
    public class Personajes
    {
        public string name;
        public int lvl;
    }

    [System.Serializable]
    public class PersonajesList
    {
        public Personajes[] personajes;
    }
    protected virtual void Start()
    {
        dropdownPJ1.ClearOptions();
        dropdownPJ2.ClearOptions();
        PersonajesList loadedData = JsonUtility.FromJson<PersonajesList>(usuarios.text);
        var dropdownOptions = new List<string>();
        foreach (Personajes personaje in loadedData.personajes)
        {

            string characterInfo = personaje.name + " (Lvl: " + personaje.lvl + ")";
            dropdownOptions.Add(characterInfo);
         
        }
        dropdownPJ1.AddOptions(dropdownOptions);
        dropdownPJ2.AddOptions(dropdownOptions);


    }
    private void Update()
    {
        OnDropdownValueChanged();
    }
    public void OnDropdownValueChanged()
    {
        int selectedIndex1 = dropdownPJ1.value;
        int selectedIndex2 = dropdownPJ2.value;

        PlayerPrefs.SetInt("ID1", selectedIndex1);
        PlayerPrefs.SetInt("ID2", selectedIndex2);
    }

}
```

<h2>3.4.2 El script ChangeScene.cs</h2>
En este fichero cs se encuentra la función Volver() que se le pasa la pantalla CombatSystem al OnClick() de los botones necesarios. Un ejemplo de su estructura sería el siguiente:

```csharp
public class ChangeScene : MonoBehaviour
{
    public void Volver(string pantallas)
    {
        SceneManager.LoadScene("Scenes/"+pantallas);
       
    }
}
```

<h2>3.5 CombatSystem</h2>
La pantalla de CombatSystem, es donde se desarrolla el combate de 2vs2 utilizado para la historia, se ha desarrollado a través de un canvas, un elemento imagen donde se inserta una imagen como fondo, un Panel donde se visualizarian los mensajes informativos del combate, un Prefab para cada personaje que es un StatsPanel (Lugar donde aparecen las estadisticas de los personajes), un Panel donde aparecerán los botones con las habilidades de los personajes vinculadas, otro Panel donde aparecerán los botones para seleccionar los enemigos si se trata de una acción que solo funciona a un personaje, un GameObject por cada personaje el cual tendrá otro GameObject que tendrá las habilidades de los personajes, y por ultimo un componente imagen por cada enemigo para posicionarlos en una plataforma en la pantalla.

<h2>3.5.1 El script StatusPanel.cs</h2>
En este fichero cs se encuentra la función SetStats() que recoge el nombre y las estadisticas del personaje en cuestión y muestra en el prefab de cada personaje el nombre, el nivel y la vida al llamar a la función SetHealth() que también está en este script. Esta función escribe en el StausPanel la vida máxima y la vida actual del personaje y según el porcentaje cambia el color de la barra de vida. Un ejemplo de su estructura sería el siguiente:

```csharp
public class StatusPanel : MonoBehaviour
{
    public Text nameLabel;
    public Text levelLabel;
    public Slider healthSlider;
    public Image healthSliderBar;
    public Text healthLabel;

    public void SetStats(string name, Stats stats)
    {
        this.nameLabel.text = name;

        this.levelLabel.text = $"N. {stats.level}";
        this.SetHealth(stats.health, stats.maxHealth);
    }

    public void SetHealth(float health, float maxHealth)
    {
        this.healthLabel.text = $"{Mathf.RoundToInt(health)} / {Mathf.RoundToInt(maxHealth)}";
        float percentage = health / maxHealth;
        Color _orange = new Color(1.0f, 0.64f, 0.0f);

        this.healthSlider.value = percentage;


        if (percentage > 0.50f)
        {
            this.healthSliderBar.color = Color.green;
        }

        if (percentage > 0.33f && percentage <= 0.50f)
        {
            this.healthSliderBar.color = Color.yellow;
        }

        if (percentage < 0.33f)
        {
            this.healthSliderBar.color = Color.red;
        }
    }
}
```

<h2>3.5.1 El script PlayerSkillPanel.cs</h2>
En este fichero cs se encuentra la función ConfigureButton() que configura los botones añadiendo el nombre de la habilidad y activandolos, también tenemos la función OnSkillButtonClick() que hara que se ejecute la habilidad. Tenemos la función ShowForPlayer() que le mostrará al jugador el Panel de habilidades, y para finalizar tenemos la función Hide() para desactivar los botones y el panel. Un ejemplo de su estructura sería el siguiente:

```csharp
public class PlayerSkillPanel : MonoBehaviour
{
    public GameObject[] skillButtons;
    public Text[] skillButtonLabels;

    private PlayerFighter targetFigther;

    void Awake()
    {
        this.Hide();
    }

    public void ConfigureButton(int index, string skillName)
    {
        this.skillButtons[index].SetActive(true);
        this.skillButtonLabels[index].text = skillName;
    }

    public void OnSkillButtonClick(int index)
    {
        this.targetFigther.ExecuteSkill(index);
    }

    public void ShowForPlayer(PlayerFighter newTarget)
    {
        this.gameObject.SetActive(true);

        this.targetFigther = newTarget;
    }

    public void Hide()
    {
        this.gameObject.SetActive(false);

        foreach (var btn in this.skillButtons)
        {
            btn.SetActive(false);
        }
    }
}
```

<h2>3.5.2 El script EnemiesPanel.cs</h2>
En este fichero cs se encuentra la función OnTargetButtonClick() que recoge los posibles objetivos de la habilidad y selecciona y ataca al escogido. Tenemos la función Show() que muestra el panel, recoge los posibles objetivos y en base a un foreach se añaden los botones para cada uno de los objetivos y se inserta su nombre, asi mismo tenemos una función Hide() para desactivar tanto el panel como los botones. En la siguiente función ActivateNextButton() tenemos el código que usamos para activar los botones en la función Show() clona el boton de ejemplo y se añade como un nuevo boton disponible con la función InsertNewButton() la cual le añade un listener para llamar a la función OnTargetButtonClick(). Un ejemplo de su estructura sería el siguiente:

```csharp
public class EnemiesPanel : MonoBehaviour
{
    public GameObject sampleButton;

    private PlayerFighter targetFighter;
    private List<Fighter> targets;

    private List<EnemyButtonUI> buttons;

    private float baseHeight;
    private RectTransform rectTransform;

    void Awake()
    {
        this.targets = new List<Fighter>();
        this.buttons = new List<EnemyButtonUI>();

        this.rectTransform = this.GetComponent<RectTransform>();
        this.baseHeight = this.rectTransform.rect.height;

        // Añadimos el botón de ejemplo como el primer botón disponible
        EnemyButtonUI btn = this.InsertNewButton(this.sampleButton, 0);
        btn.Hide();

        this.Hide();
    }

    public void OnTargetButtonClick(int index)
    {
        Fighter target = this.targets[index];

        this.targetFighter.SetTargetAndAttack(target);
    }

    public void Show(PlayerFighter playerFighter, Fighter[] targets)
    {
        this.gameObject.SetActive(true);

        this.targetFighter = playerFighter;

        int btnIndex = 0;

        foreach (var target in targets)
        {
            EnemyButtonUI btn = this.ActivateNextButton(btnIndex);
            btn.SetText(target.idName);

            this.targets.Add(target);

            btnIndex++;
        }

        this.rectTransform.sizeDelta = new Vector2(
            this.rectTransform.rect.width,
            this.baseHeight
        );
    }

    public void Hide()
    {
        this.gameObject.SetActive(false);

        foreach (var btn in this.buttons)
        {
            btn.Hide();
        }

        this.targets.Clear();
    }

    private EnemyButtonUI ActivateNextButton(int index)
    {
        foreach (var btn in this.buttons)
        {
            if (btn.index == index)
            {
                btn.Show();
                return btn;
            }
        }

        // Clonamos el botón de ejemplo
        GameObject btnGO = Instantiate(this.sampleButton);
        btnGO.transform.SetParent(this.transform);
        btnGO.transform.localScale = Vector3.one;

        // Lo añadimos como nuevo botón disponible
        EnemyButtonUI but = this.InsertNewButton(btnGO, index);
        but.Show();

        return but;
    }

    private EnemyButtonUI InsertNewButton(GameObject btnGO, int index)
    {
        EnemyButtonUI btn = new EnemyButtonUI(btnGO, index);
        btn.button.onClick.AddListener(() => { this.OnTargetButtonClick(btn.index); });

        this.buttons.Add(btn);

        return btn;
    }
}
```

<h2>3.5.3 El script Fighter.cs</h2>
En este fichero cs se encuentra la parte principal respecto a los personajes. Recogemos los datos de los personajes. La primera función que tenemos es una función booleana llamada isAlive() la cual se asegura de revisar si un personaje esta vivo cada vez que se llama a la función. En el método Start() asigna las estadisticas y el nombre al Panel de los aliados y enemigos. La siguiente función es AutoConfigureSkillTargeting() lo que hace este método es determinar a quién está dirigida la habilidad; tenemos un "switch" con varias opciones, una opción "AUTO", otra "ALL_ALLIES" que dirige la habilidad a todos los aliados ("Heal, regeneraciones, subida de estadísticas") y "ALL_OPPONENTS" que dirige la habilidad a todos los enemigos. En la función GetSkillTargets() tenemos lo mismo pero en habilidades que debemos seleccionar al enemigo, recoge la lista de posibles selecciones del "CombatManager" comprueba que están vivos y se ejecuta la acción. Ahora tenemos la función Die() desactiva todos los GameObjects del personaje que haya muerto. La siguiente función se llama ModifyHealth() en este método tomamos la vida del personaje y utilizamos un "Mathf.Clamp" que fija el valor dado entre los valores mínimo y máximo de "float". Después de esto hacemos un Mathf.Round para colocar la vida en un número redondo y la ponemos en el personaje. Al final tenemos un "if" por si el personaje muere, que lo que va a hacer es invocar la animación de muerte e invocar el método "Die" que ha sido explicado antes. Ahora tenemos la función GetCurrentStats() que es el que hace los cambios de subida y bajada de estadisticas. Y para acabar tenemos GetCurrentStatusCondition() que básicamente lo que hace es que si el personaje tiene una condición y expira ahora destruye el "GameObject" y declara "StatusCondition" como "null" y lo devuelve. Un ejemplo de su estructura sería el siguiente:

```csharp
public abstract class Fighter : MonoBehaviour
{
    public Team team;
    public TextAsset usuarios;
    public StatusPanel ally;
    public StatusPanel ally2;
    public Animator animator;
    public GameObject cloud;

    [System.Serializable]
    public class Personajes
    {
        public string name;
        public int lvl;
        public StatsPj stats;
    }

    [System.Serializable]
    public class StatsPj
    {
        public int hp;
        public int def;
        public int atk;
    }


    [System.Serializable]
    public class PersonajesList
    {
        public Personajes[] personajes;

    }

    public string idName;

    public int id;

    public StatusPanel statusPanel;

    public CombatManager combatManager;

    public List<StatusMod> statusMods;

    protected Stats stats;

    protected Skill[] skills;

    public StatusCondition statusCondition;

    public bool isAlive
    {
        get => this.stats.health > 0;
    }

    protected virtual void Start()
    {
        if (team == Team.PLAYERS)
        {
            int character1 = PlayerPrefs.GetInt("ID1");
            int character2 = PlayerPrefs.GetInt("ID2");

            PersonajesList loadedData = JsonUtility.FromJson<PersonajesList>(usuarios.text);

            var pj = loadedData.personajes[character1];

            this.ally.SetStats(loadedData.personajes[character1].name, new Stats(pj.lvl, pj.stats.hp, pj.stats.atk, pj.stats.def, 20));

            pj = loadedData.personajes[character2];
            this.ally2.SetStats(loadedData.personajes[character2].name, new Stats(pj.lvl, pj.stats.hp, pj.stats.atk, pj.stats.def, 20));            
            
            this.skills = this.GetComponentsInChildren<Skill>();

            this.statusMods = new List<StatusMod>();
		}
		else
		{
            this.statusPanel.SetStats(idName, this.stats);

            this.skills = this.GetComponentsInChildren<Skill>();

            this.statusMods = new List<StatusMod>();
        }
    }


    protected void AutoConfigureSkillTargeting(Skill skill)
    {
        skill.SetEmitter(this);

        switch (skill.targeting)
        {
            case SkillTargeting.AUTO:
                skill.AddReceiver(this);
                break;
            case SkillTargeting.ALL_ALLIES:
                Fighter[] allies = this.combatManager.GetAllyTeam();
                foreach (var receiver in allies)
                {
                    skill.AddReceiver(receiver);
                }

                break;
            case SkillTargeting.ALL_OPPONENTS:
                Fighter[] enemies = this.combatManager.GetOpposingTeam();
                foreach (var receiver in enemies)
                {
                    skill.AddReceiver(receiver);
                }
                break;

            case SkillTargeting.SINGLE_ALLY:
            case SkillTargeting.SINGLE_OPPONENT:
                throw new System.InvalidOperationException("Unimplemented! This skill needs manual targeting.");
        }
    }

    protected Fighter[] GetSkillTargets(Skill skill)
    {
        switch (skill.targeting)
        {
            case SkillTargeting.AUTO:
            case SkillTargeting.ALL_ALLIES:
            case SkillTargeting.ALL_OPPONENTS:
                throw new System.InvalidOperationException("Unimplemented! This skill doesn't need manual targeting.");

            case SkillTargeting.SINGLE_ALLY:
                return this.combatManager.GetAllyTeam();
            case SkillTargeting.SINGLE_OPPONENT:
                return this.combatManager.GetOpposingTeam();
        }

        // Esto no debería ejecutarse nunca pero hay que ponerlo para hacer al compilador feliz.
        throw new System.InvalidOperationException("Fighter::GetSkillTargets. Unreachable!");
    }

    protected void Die()
    {
        this.cloud.gameObject.SetActive(false);
        this.statusPanel.gameObject.SetActive(false);
        this.gameObject.SetActive(false);
    }    

    public void ModifyHealth(float amount)
    {
        this.stats.health = Mathf.Clamp(this.stats.health + amount, 0f, this.stats.maxHealth);

        this.stats.health = Mathf.Round(this.stats.health);
        this.statusPanel.SetHealth(this.stats.health, this.stats.maxHealth);

        if (this.isAlive == false)
        {
            animator.Play("Death");
            Invoke("Die", 0.75f);
        }
    }

    public Stats GetCurrentStats()
    {
        Stats modedStats = this.stats;

        foreach (var mod in this.statusMods)
        {
            modedStats = mod.Apply(modedStats);
        }

        return modedStats;
    }

    public StatusCondition GetCurrentStatusCondition()
    {
        if (this.statusCondition != null && this.statusCondition.hasExpired)
        {
            Destroy(this.statusCondition.gameObject);
            this.statusCondition = null;
        }

        return this.statusCondition;
    }

    public abstract void InitTurn();
}
```

<h2>3.5.4 El script PlayerFighter.cs</h2>
En fichero cs es exclusivo para los personajes del usuario. En el método Awake() Recogemos los ID que hemos pasado anteriormente en la PantallaEleccion1 y dependiendo de un id independiente de esta pantalla asigna las estadisticas de los personajes aliados. El método InitTurn() llama al método ShowForPlayer() y muestra el panel de habilidades al usuario. En el siguiente método ExecuteSkill() recoge la lista de enemigos para enviarla al EnemiesPanel y asi que nos salgan los enemigos a seleccionar al usar una habilidad. Por último tenemos SetTargetAndAttack() recoge el enemigo seleccionado y la envia al CombatManager para ejecutar la habilidad y después oculta los paneles. Un ejemplo de su estructura sería el siguiente:

```csharp
public class PlayerFighter : Fighter
{
    
    [Header("UI")]
    public PlayerSkillPanel skillPanel;
    public EnemiesPanel enemiesPanel;

    private Skill skillToBeExecuted;

    void Awake()
    {
        PersonajesList loadedData = JsonUtility.FromJson<PersonajesList>(usuarios.text);
        
        int character1 = PlayerPrefs.GetInt("ID1");
        int character2 = PlayerPrefs.GetInt("ID2");

        if (id == 0)
		{
            // Estadísticas para el primer personaje (id = 0)
            int lvl1 = loadedData.personajes[character1].lvl;
            int hp1 = loadedData.personajes[character1].stats.hp;
            int atk1 = loadedData.personajes[character1].stats.atk;
            int def1 = loadedData.personajes[character1].stats.def;
            this.stats = new Stats(lvl1, hp1, atk1, def1, 20);
		}
		else if(id == 1)
        {
            // Estadísticas para el segundo personaje (id = 1)
            int lvl2 = loadedData.personajes[character2].lvl;
            int hp2 = loadedData.personajes[character2].stats.hp;
            int atk2 = loadedData.personajes[character2].stats.atk;
            int def2 = loadedData.personajes[character2].stats.def;
            this.stats = new Stats(lvl2, hp2, atk2, def2, 20);
        }

    }

    public override void InitTurn()
    {
        this.skillPanel.ShowForPlayer(this);

        for (int i = 0; i < this.skills.Length; i++)
        {
            this.skillPanel.ConfigureButton(i, this.skills[i].skillName);
        }
    }

    /// ================================================
    /// <summary>
    /// Se llama desde EnemiesPanel.
    /// </summary>
    /// <param name="index"></param>
    public void ExecuteSkill(int index)
    {
        this.skillToBeExecuted = this.skills[index];
        this.skillToBeExecuted.SetEmitter(this);

        if (this.skillToBeExecuted.needsManualTargeting)
        {
            Fighter[] receivers = this.GetSkillTargets(this.skillToBeExecuted);
            this.enemiesPanel.Show(this, receivers);
        }
        else
        {
            this.AutoConfigureSkillTargeting(this.skillToBeExecuted);

            this.combatManager.OnFighterSkill(this.skillToBeExecuted);
            this.skillPanel.Hide();
        }
    }

    public void SetTargetAndAttack(Fighter enemyFigther)
    {
        this.skillToBeExecuted.AddReceiver(enemyFigther);

        this.combatManager.OnFighterSkill(this.skillToBeExecuted);

        this.skillPanel.Hide();
        this.enemiesPanel.Hide();
    }
}
```

<h2>3.5.5 El script EnemyFighter.cs</h2>
En fichero cs es exclusivo para los personajes del enemigo. En el método Awake() se asignan las estadisticas de los personajes enemigos según la fase de la batalla en la que estés. El método InitTurn() activa la corutina IA() que esta coge las habilidades que tiene el enemigo y coge un número aleatorio del 0 en el ".length" de las habilidades, si la habilidad que elige necesita seleccionar a un enemigo entra en un "if" en el que recoge la lista de personajes y realiza otro número aleatorio como antes. Un ejemplo de su estructura sería el siguiente:

```csharp
public class EnemyFighter : Fighter
{
    void Awake()
    {
        int sceneId = PlayerPrefs.GetInt("ID");
		switch (sceneId)
		{
            case 1:
                this.stats = new Stats(10, 10, 10, 10, 10);
                break;
            case 2:
                this.stats = new Stats(12, 12, 12, 12, 12);
                break;
            case 3:
                this.stats = new Stats(20, 20, 20, 20, 20);
                break;
            case 4:
                this.stats = new Stats(25, 27, 30, 31, 30);
                break;
            case 5:
                this.stats = new Stats(30, 40, 32, 33, 31);
                break;
            case 6:
                this.stats = new Stats(40, 50, 50, 50, 40);
                break;
            case 7:
                this.stats = new Stats(50, 75, 75, 75, 50);
                break;
            case 8:
                this.stats = new Stats(60, 100, 105, 75, 50);
                break;
            case 9:
                this.stats = new Stats(65, 150, 105, 75, 50);
                break;
            case 10:
                this.stats = new Stats(70, 200, 105, 75, 50);
                break;

        }
    }

    public override void InitTurn()
    {
        StartCoroutine(this.IA());
    }

    IEnumerator IA()
    {
        yield return new WaitForSeconds(1f);

        Skill skill = this.skills[Random.Range(0, this.skills.Length)];
        skill.SetEmitter(this);

        if (skill.needsManualTargeting)
        {
            Fighter[] targets = this.GetSkillTargets(skill);

            Fighter target = targets[Random.Range(0, targets.Length)];

            skill.AddReceiver(target);
        }
        else
        {
            this.AutoConfigureSkillTargeting(skill);
        }

        this.combatManager.OnFighterSkill(skill);
        
    }
}
```

<h2>3.5.6 El script CombatManager.cs</h2>
Para empezar coge todos los personajes y enemigos, irá a una función llamada SortFightersBySpeed() la cual ordenará los turnos de todos.
Después de esto iniciará la función MakeTeams() en la que básicamente, declara 2 listas de "Fighter" una para los aliados y otra para los enemigos, cuando un "Fighter" tenga la etiqueta "Team.PLAYERS" se añadirá a la lista de aliados y cuando tenga la etiqueta "Team.ENEMIES" se añadirá a la lista de enemigos.
Tras esta preparación entra en una nueva "Coroutine" que es CombatLoop() la cual como su nombre dice es un bucle del combate hasta que se dé la condición para salir. A la vez que entramos en esta "Coroutine" entramos en la etiqueta "CombatStatus.NEXT_TURN".
Todas las etiquetas de "CombatStatus" están en un "switch" dentro de CombatLoop(). En "CombatStatus.NEXT_TURN" determina dentro de un "do while" al que le corresponde el turno, si al que le tocaría no está vivo entonces sale.
Asimismo cambiamos de etiqueta y vamos a "CombatStatus.CHECK_FIGHTER_STATUS_CONDITION"; aquí obtenemos el "Fighter" que le toca en ese turno y su condición ("Stun, Regeneration"), si tiene alguna condición se ejecuta y hace la acción, entra en un "while(true)" que muestra el mensaje por pantalla; si no hay más mensajes que mostrar saldrá del bucle.
Después de esto miramos si la condición te bloquea el turno y si se bloquea saltamos todos los pasos y vamos a "CombatStatus.CHECK_FOR_VICTORY" que revisará si están vivos o muertos los jugadores y poder declarar una victoria o derrota, si no hay ninguna de estas dos vuelve a "CombatStatus.NEXT_TURN".
Ahora bien, si no tiene ninguna condición a aplicar a "CombatStatus.CHECK_FIGHTER_STATUS_CONDITION" pasa a otra etiqueta llamada "CombatStatus.WAITING_FOR_FIGHTER", esta etiqueta únicamente espera que el jugador o la "IA" haga alguna acción, cuando realiza una acción s ejecuta la función OnFighterSkill() y pasa a otra etiqueta llamada "CombatStatus.FIGHTER_ACTION". Lo primero que hace es mostrar un mensaje de quien ha utilizado una habilidad y cuál es. Ejecutamos la habilidad y esperamos la animación. Después de esto vamos a la etiqueta "CombatStatus.CHECK_ACTION_MESSAGES", aquí revisamos si tenemos un nuevo mensaje a mostrar, por ejemplo, si utilizas una habilidad "Stun" el primer mensaje será ("Player uses Stun") y el segundo mensaje será ("Enemy is stunned").
Cuando no haya más mensajes a mostrar volvemos a "CombatStatus.CHECK_FOR_VICTORY" y así hasta que termine el combate. Un ejemplo de su estructura sería el siguiente:

```csharp
public enum CombatStatus
{
    WAITING_FOR_FIGHTER,
    FIGHTER_ACTION,
    CHECK_ACTION_MESSAGES,
    CHECK_FOR_VICTORY,
    NEXT_TURN,
    CHECK_FIGHTER_STATUS_CONDITION
}

public class CombatManager : MonoBehaviour
{
    private Fighter[] playerTeam;
    private Fighter[] enemyTeam;

    private Fighter[] fighters;
    private int fighterIndex;

    private bool isCombatActive;

    private CombatStatus combatStatus;

    private Skill currentFighterSkill;

    private List<Fighter> returnBuffer;

    void Start()
    {
        this.returnBuffer = new List<Fighter>();

        this.fighters = GameObject.FindObjectsOfType<Fighter>();

        this.SortFightersBySpeed();
        this.MakeTeams();

        LogPanel.Write("Battle initiated.");

        this.combatStatus = CombatStatus.NEXT_TURN;

        this.fighterIndex = -1;
        this.isCombatActive = true;
        StartCoroutine(this.CombatLoop());
    }

    private void SortFightersBySpeed()
    {
        bool sorted = false;
        while (!sorted)
        {
            sorted = true;

            for (int i = 0; i < this.fighters.Length - 1; i++)
            {
                Fighter a = this.fighters[i];
                Fighter b = this.fighters[i + 1];

                float aSpeed = a.GetCurrentStats().speed;
                float bSpeed = b.GetCurrentStats().speed;

                if (bSpeed > aSpeed)
                {
                    this.fighters[i] = b;
                    this.fighters[i + 1] = a;

                    sorted = false;
                }
            }
        }
    }

    private void MakeTeams()
    {
        List<Fighter> playersBuffer = new List<Fighter>();
        List<Fighter> enemiesBuffer = new List<Fighter>();

        foreach (var fgtr in this.fighters)
        {
            if (fgtr.team == Team.PLAYERS)
            {
                playersBuffer.Add(fgtr);
            }
            else if (fgtr.team == Team.ENEMIES)
            {
                enemiesBuffer.Add(fgtr);
            }

            fgtr.combatManager = this;
        }

        this.playerTeam = playersBuffer.ToArray();
        this.enemyTeam = enemiesBuffer.ToArray();
    }

    IEnumerator CombatLoop()
    {
        while (this.isCombatActive)
        {
            switch (this.combatStatus)
            {
                case CombatStatus.WAITING_FOR_FIGHTER:

                    yield return null;
                    break;

                case CombatStatus.FIGHTER_ACTION:
                    LogPanel.Write($"{this.fighters[this.fighterIndex].idName} uses {currentFighterSkill.skillName}.");

                    yield return null;

                    // Executing fighter skill
                    currentFighterSkill.Run();

                    // Wait for fighter skill animation
                    yield return new WaitForSeconds(currentFighterSkill.animationDuration);
                    
                    this.combatStatus = CombatStatus.CHECK_ACTION_MESSAGES;

                    break;
                case CombatStatus.CHECK_ACTION_MESSAGES:
                    string nextMessage = this.currentFighterSkill.GetNextMessage();

                    if (nextMessage != null)
                    {
                        LogPanel.Write(nextMessage);
                        yield return new WaitForSeconds(2f);
                    }
                    else
                    {
                        this.currentFighterSkill = null;
                        this.combatStatus = CombatStatus.CHECK_FOR_VICTORY;
                        yield return null;
                    }
                    break;

                case CombatStatus.CHECK_FOR_VICTORY:
                    bool arePlayersAlive = false;
                    foreach (var figther in this.playerTeam)
                    {
                        arePlayersAlive |= figther.isAlive;
                    }

                    bool areEnemiesAlive = false;
                    foreach (var figther in this.enemyTeam)
                    {
                        areEnemiesAlive |= figther.isAlive;
                    }

                    bool victory = areEnemiesAlive == false;
                    bool defeat  = arePlayersAlive == false;

                    if (victory)
                    {
                        LogPanel.Write("Victoria!");
                        this.isCombatActive = false;
                        SceneManager.LoadScene("Scenes/PantallaHistoria");
                    }

                    if (defeat)
                    {
                        LogPanel.Write("Derrota!");
                        this.isCombatActive = false;
                        SceneManager.LoadScene("Scenes/PantallaHistoria");
                    }

                    if (this.isCombatActive)
                    {
                        this.combatStatus = CombatStatus.NEXT_TURN;
                    }

                    yield return null;
                    break;
                case CombatStatus.NEXT_TURN:
                    
                    yield return new WaitForSeconds(1f);

                    Fighter current = null;

                    do {
                        this.fighterIndex = (this.fighterIndex + 1) % this.fighters.Length;

                        current = this.fighters[this.fighterIndex];
                    } while (current.isAlive == false);

                    this.combatStatus = CombatStatus.CHECK_FIGHTER_STATUS_CONDITION;

                    break;

                case CombatStatus.CHECK_FIGHTER_STATUS_CONDITION:
                    var currentFighter = this.fighters[this.fighterIndex];

                    var statusCondition = currentFighter.GetCurrentStatusCondition();

                    if (statusCondition != null)
                    {
                        statusCondition.Apply();

                        while (true)
                        {
                            string nextSCMessage = statusCondition.GetNextMessage();
                            if (nextSCMessage == null)
                            {
                                break;
                            }

                            LogPanel.Write(nextSCMessage);
                            yield return new WaitForSeconds(2f);
                        }

                        if (statusCondition.BlocksTurn())
                        {
                            this.combatStatus = CombatStatus.CHECK_FOR_VICTORY;
                            break;
                        }
                    }

                    LogPanel.Write($"{currentFighter.idName} has the turn.");
                    currentFighter.InitTurn();

                    this.combatStatus = CombatStatus.WAITING_FOR_FIGHTER;
                    break;
            }
        }
    }

    public Fighter[] FilterJustAlive(Fighter[] team)
    {
        this.returnBuffer.Clear();

        foreach (var fgtr in team)
        {
            if (fgtr.isAlive)
            {
                this.returnBuffer.Add(fgtr);
            }
        }

        return this.returnBuffer.ToArray();
    }

    public Fighter[] GetOpposingTeam()
    {
        Fighter currentFighter = this.fighters[this.fighterIndex];

        Fighter[] team = null;
        if (currentFighter.team == Team.PLAYERS)
        {
            team = this.enemyTeam;
        }
        else if (currentFighter.team == Team.ENEMIES)
        {
            team = this.playerTeam;
        }

        return this.FilterJustAlive(team);
    }

    public Fighter[] GetAllyTeam()
    {
        Fighter currentFighter = this.fighters[this.fighterIndex];

        Fighter[] team = null;
        if (currentFighter.team == Team.PLAYERS)
        {
            team = this.playerTeam;
        }
        else
        {
            team = this.enemyTeam;
        }

        return this.FilterJustAlive(team);
    }

    public void OnFighterSkill(Skill skill)
    {
        this.currentFighterSkill = skill;
        this.combatStatus = CombatStatus.FIGHTER_ACTION;
    }
}
```


<h2>3.6 PantallaBosses</h2>
La PantallaBosses, es el menú donde se selecciona el boss contra el que quieres combatir, hay 3 tipos. Se ha desarrollado a través de un canvas, un elemento imagen donde se inserta una imagen como fondo, un Panel donde podremos ver la información del usuario, un Boton para Volver al menú principal y un GameObject vacio donde agrupar los botones que nos llevan a cada uno de los bosses.


<h2>3.7 PantallaEleccion2</h2>
La PantallaEleccion2, es el menú donde se selecciona los personajes para luchar contra el boss contra que quieres combatir. Se ha desarrollado de la misma manera que la PantallaEleccion1 con una diferencia y es el script ChangeSceneBoss.cs.

<h2>3.7.1 El script ChangeSceneBoss.cs</h2>
Para empezar recoge el id que le hemos pasado al seleccionar el boss, y ejecutara el método ChangeScene() que nos redirigira a una pantalla u otra según el boss seleccionado. Un ejemplo de su estructura sería el siguiente:

```csharp
public class ChangeSceneBoss : MonoBehaviour
{
    public void ChangeScene()
    {
        int boss = PlayerPrefs.GetInt("ID");
        if (boss == 8) {
            SceneManager.LoadScene("Scenes/CombatBoss1");
        }
        else if (boss == 9)
        {
            SceneManager.LoadScene("Scenes/CombatBoss2");
        }
        else if (boss == 10)
        {
            SceneManager.LoadScene("Scenes/CombatBoss3");
        }
    }
}
```

<h2>3.8 CombatBoss1, CombatBoss2, CombatBoss3</h2>
Estas pantallas, Son los sistemas de combate contra bosses. Se ha desarrollado de la misma manera que la pantalla CombatSystem solo que ahora tenemos un solo enemigo.


<h2>3.9 PantallaGacha</h2>
La PantallaGacha, es el menú donde se consiguen los personajes de forma aleatoria. Se ha desarrollado a través de un canvas, un elemento imagen donde se inserta una imagen como fondo, un Panel donde podremos ver la información del usuario, un Boton para sacar un personaje, un Panel donde nos saldrá la información del personaje que hemos obtenido el cual tiene un boton para ocultar el panel y por ultimo tenemos el boton para volver al menú principal.

<h2>3.9.1 El script Gacha.cs</h2>
El Gacha es un script de Unity que implementa un sistema de obtención de personajes aleatorios en un juego. Para empezar coge todos los personajes y los datos del usuario e irá a una función llamada SelectRandomChracter() que lo que hace es coger el JSON de los personajes, crea un número “random” entre el 0 y el número máximo de los personajes.
Así pues, tomamos toda la información del personaje de la clase "Character". Para obtener las estadísticas, hacemos un llamamiento a la clase "Stats", y para añadir el nuevo personaje, debemos realizar llamadas a las clases "Character" y "Stats" al mismo tiempo.
Después, iremos a la función AddCharacter(), enviándole el objeto del nuevo personaje y el nombre del personaje.
Dentro de la función, primero leeremos el JSON de usuario y añadiremos un nuevo personaje a la sección de personajes. Después, guardaremos el archivo e iremos a la función "showPopUp()", pasándole el nombre del personaje que hemos añadido. Dentro de la función, activaremos el panel para que sea visible y en el texto añadiremos el nombre del nuevo personaje aleatorio que ha salido en el gacha anterior.
También existe una función llamada "closePanel()" que será llamada desde el botón del "Pop up" para hacer que el panel sea invisible. Un ejemplo de su estructura sería el siguiente:

```csharp
public class Gacha : MonoBehaviour
{
    private List<Character> characters;
    public TextAsset personajes;
    public TMP_Text popUpText;
    public GameObject panel;

    [System.Serializable]
    public class User
    {
        public string usuario;
        public string email;
        public string password;
        public string nivel;
        public string monedas;
        public string gemas;
        public List<Character> personajes;
    }

    [System.Serializable]
    public class CharactersData
    {
        public List<Character> personajes;
    }

    [System.Serializable]
    public class Character
    {
        public string name;
        public string type;
        public string lore;
        public int lvl;
        public Stats stats;
        public Skills Skills;
    }

    [System.Serializable]
    public class Stats
    {
        public int hp;
        public int defense;
        public int atk;
        public int speed;
    }

    [System.Serializable]
    public class Skills
    {
        public Skill passive;
        public Skill skill1;
        public Skill skill2;
        public Skill Ulti;
    }

    [System.Serializable]
    public class Skill
    {
        public int id_skills;
        public string type_skill;
        public string name;
        public string description;
    }

    private string filePath;

    private void Start()
    {
        filePath = Application.dataPath + "/Resources/usuarios.json";
        string jsonString = File.ReadAllText(filePath);
        Debug.Log(jsonString);
        panel.SetActive(false);
    }

    public void SelectRandomCharacter()
    {
        characters = JsonUtility.FromJson<CharactersData>(personajes.text).personajes;
        int randomIndex = Random.Range(0, characters.Count);
        Character randomCharacter = characters[randomIndex];

        Character newCharacter = new Character();
        string nombrePersonajes = randomCharacter.name;
        newCharacter.name = randomCharacter.name;
        newCharacter.type = randomCharacter.type;
        newCharacter.lore = randomCharacter.lore;
        newCharacter.lvl = randomCharacter.lvl;

        newCharacter.stats = new Stats();
        newCharacter.stats.hp = randomCharacter.stats.hp;
        newCharacter.stats.defense = randomCharacter.stats.defense;
        newCharacter.stats.atk = randomCharacter.stats.atk;
        newCharacter.stats.speed = randomCharacter.stats.speed;

        newCharacter.Skills = new Skills();

        newCharacter.Skills.skill1 = new Skill();
        newCharacter.Skills.skill1.id_skills = randomCharacter.Skills.skill1.id_skills;
        newCharacter.Skills.skill1.type_skill = randomCharacter.Skills.skill1.type_skill;
        newCharacter.Skills.skill1.name = randomCharacter.Skills.skill1.name;
        newCharacter.Skills.skill1.description = randomCharacter.Skills.skill1.description;

        newCharacter.Skills.skill2 = new Skill();
        newCharacter.Skills.skill2.id_skills = randomCharacter.Skills.skill2.id_skills;
        newCharacter.Skills.skill2.type_skill = randomCharacter.Skills.skill2.type_skill;
        newCharacter.Skills.skill2.name = randomCharacter.Skills.skill2.name;
        newCharacter.Skills.skill2.description = randomCharacter.Skills.skill2.description;

        newCharacter.Skills.Ulti = new Skill();
        newCharacter.Skills.Ulti.id_skills = randomCharacter.Skills.Ulti.id_skills;
        newCharacter.Skills.Ulti.type_skill = randomCharacter.Skills.Ulti.type_skill;
        newCharacter.Skills.Ulti.name = randomCharacter.Skills.Ulti.name;
        newCharacter.Skills.Ulti.description = randomCharacter.Skills.Ulti.description;

        AddCharacterJSON(newCharacter, nombrePersonajes);
    }

    private void AddCharacterJSON(Character newCharacter, string nombrePersonajes)
    {
        string jsonString = File.ReadAllText(filePath);

        User currentUser = JsonUtility.FromJson<User>(jsonString);
        currentUser.personajes.Add(newCharacter);

        string updatedJson = JsonUtility.ToJson(currentUser);
        File.WriteAllText(filePath, updatedJson);

        showPopUp(nombrePersonajes);
    }

    public void showPopUp(string nombrePersonajes)
    {
        panel.SetActive(true);
        popUpText.text = "Personaje: " + nombrePersonajes;
    }

    public void closePanel()
    {
        panel.SetActive(false);
    }
}
```
