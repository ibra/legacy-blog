+++
title = "How I Made YourShot's Ability System In Unity"
date = 2020-12-21

[extra]
author = "Ibrahim"

[taxonomies]
categories = ["YourShot"]
+++

Over the past few days, ive been working on _YourShot's_ Ability system. I tried looking online and theres not really enough <!-- more --> information for a newbie to make an informed decision about how they should approach going about this. In the end I personally settled on a mix of inheritance and scriptable objects. The two objectives for this Ability System for me personally were:

- Making sure that any sort of ability can be created with the system.
- Making sure that these abilities can be created efficiently and without refactoring.

Before I jump in though, I wanted to say that this is **not** a step-by-step tutorial. Its more an abstracted version of my approach (even though it will still have a detailed explanation) so you can have a general idea of how to approach making an Ability System.

## Code Structure

First of all we shall need an `Ability.cs` class.

```cs
using UnityEngine;
using System.Collections;

namespace YourShot.AbilitySystem
{
    public abstract class Ability : ScriptableObject
    {

        public string name = "New Ability";
        public Sprite sprite;
        public AudioClip sound;
        public float baseCoolDown = 1f;

        public abstract void Initialize(GameObject obj);
        public abstract void TriggerAbility();
    }
}
```

You might or might not understand some stuff right off the bat, so let me explain.
First of all, this line:

```cs
public abstract class Ability : ScriptableObject
```

This class is basically deriving from ScriptableObject. If you dont know what a ScriptableObject is, I'd recommend watching [this video](https://www.youtube.com/watch?v=aPXvoWVabPY) from Brackeys. If you know a bit about scriptable objects you might be wondering why we **aren't** using the CreateAssetMenu attribute.

e.g:

```cs
[CreateAssetMenu("Abilities/Ability")]
```

That is because we will be using this attribute in our **derived** classes for different abilities, since the system wouldnt really work if we used it in our abstract class.

Speaking of abstract, an `abstract` class is basically a restricted class that cannot be used to create objects, and the only way to access is, inheriting it from another class. The rest of the script is pretty self-explanatory, other than

```cs
public abstract void Foo();
```

An abstract void is basically a method that does not have a body. The body is "filled in" by the derived class.

This as of now, is just an abstract class. We're gonna create some simple derived classes in a bit.

Next, we're going to use Unity's Input System to do trigger our abilities whenever we press a button. I'm using Unity's New Input System, so this is what my ability triggering script looks like.

```cs
public class PlayerAbility : MonoBehaviour
{

    [SerializeField] private Ability primaryAbility;
    [SerializeField] private Ability secondaryAbility;
    private PlayerControls playerControls;

 private void Awake()
 {
        playerControls = new PlayerControls();
    }
 void Start()
    {
        primaryAbility.Initialize(gameObject);
        secondaryAbility.Initialize(gameObject);

        playerControls.Main.PrimaryAbility.performed += _ =>   primaryAbility.TriggerAbility();
        playerControls.Main.SecondaryAbility.performed += _ => secondaryAbility.TriggerAbility();
    }

    private void OnEnable()
    {
        playerControls.Enable();
    }
    private void OnDisable()
    {
        playerControls.Disable();
    }
}
```

However, if you're using Unity's Old Input System just replace these:

```cs
playerControls.Main.PrimaryAbility.performed += _ => primaryAbility.TriggerAbility();
```

with this (but make sure its in Update, not Start):

```cs
if(Input.GetButton("PrimaryButton")
{
  primaryAbility.TriggerAbility();
}
if(Input.GetButton("SecondaryButton")
{
  secondaryAbility.TriggerAbility();
}
```

So this is cool and all, but we cant really assign abstract classes to the inspector. So we need to create some... **D e r i v e d** Classes. We still want these classes to be as vague as possible, so as to be able to create more Abilities with less coding, because imagine actually doing effort.

So lets make a simple projectile ability.

```cs
using UnityEngine;
using System.Collections;

namespace YourShot.AbilitySystem
{

 [CreateAssetMenu(menuName = "Abilities/ProjectileAbility")]
 public class ProjectileAbility : Ability
 {

  public float projectileForce = 500f;
  public Rigidbody projectile;

  private ProjectileShootTriggerable weapon;

  public override void Initialize(GameObject obj)
  {
   weapon = obj.GetComponent<ProjectileShootTriggerable>();
   weapon.projectileForce = projectileForce;
   weapon.projectile = projectile;
  }

  public override void TriggerAbility()
  {
   weapon.TriggerFire();
  }

 }

}
```

So, this is our ProjectileAbility class. If you have keen eye, you might've noticed that we have this script called `ProjectileShootTriggerable`. Whats that all about? I'll get to it in a moment. But first, let me explain what is going on in this script.

First and foremost, we have our `ProjectileAbility` class which derives from `Ability` with a `CreateAssetMenu` attribute that we can use to create SerializeObjects in the Projects folder.

Then we have 2 `override` methods, which if you didn't notice have the same name as the methods in our original `Ability.cs` abstracted class. Basically we are overriding (as the keyword suggests) our original abstract methods, basically filling in their body.

Now, lets go back to that script you saw earlier called `ProjectileShootTriggerable` that is referenced in our `ProjectileAbility.cs` script. Here are the contents of that script:

```cs
using UnityEngine;
using System.Collections;

public class ProjectileShootTriggerable : MonoBehaviour
{

 [HideInInspector] public Rigidbody projectile;
    [HideInInspector] public float projectileForce = 250f;
 public Transform bulletSpawn;


 public void Launch()
 {

  Rigidbody bulletInstance = Instantiate(projectile, bulletSpawn.position, transform.rotation);
  clonedBullet.AddForce(bulletSpawn.transform.forward * projectileForce);
 }
}
```

You should apply this script to your Gun/Cannon/Firearm/Mass Weapon of Destruction

Then create a new Ability by Right Clicking on the Project folder, and you should be set. Like i said before, this wasn't really a complete step-by-step tutorial, but if you are intermediate, or know your way around C#, you should now (hopefully) have an idea as to how you should approach making an Ability System. If you are still facing issues though I have my socials on the home page of this blog, and you can contact me from there.
