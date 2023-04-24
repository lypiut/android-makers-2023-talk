slidenumbers: true
slide-transition: false

# [fit] Become a **Maestro** of Mobile Testing
# [fit] in **5** minutes

---

# Hello :wave:

**Romain Rivollier** - *Staff Engineer*
**Jordan Dahnoun** - *Engineer Manager*


## Helping **students** finding their first **job** on
![inline 18%](ressources/jobteaser.png)


---
# Objectives of this **talk** 

- Better understand *Shift Left* and **End-to-End testing**
- Introduce **Maestro** and how to integrate it in your processes

---

# **Shift Left** in Mobile Engineering

- Catch bugs before the **release**
- Shipping your *mobile app* with **confidence**


---
# **Shift Left** in Mobile Engineering

![inline](ressources/shift_left_before.jpg)

---
# **Shift Left** in Mobile Engineering

![inline](ressources/shift_left_after.jpg)

---

# [fit] **End to End** testing

---

# Story Time

---

# Back in the day

- Reboot **JobTeaser** mobile app in 2019
- Write it with End to End testing in mind
- Build a new test stack

---

# The stack

![inline fill](ressources/existing-stack.png)

---

# A test

![right fit](ressources/landing_jt.png)

```gherkin
@resetApp @iOS @android
Feature: [Landing] Landing

Scenario: SignIn
    Given I am on "landing" view
    When  I click on "sign in button"
    Then  I am on "sign in email" view
```

---

```typescript
interface ILandingSelectors extends SelectorCollection {
    'sign in button': Selector;
    'sign up button': Selector;
}

export abstract class Landing<T extends ILandingSelectors> extends View<T> {
    protected lists = [];
    protected widgets = [];
    protected url = undefined;
    protected navigationSteps = [
        async (): Promise<void> => {
            await this.waitForExist();
        },
    ];
}

class LandingAndroid extends Landing<typeof AndroidSelectors> {
    protected selectors = {
	    'sign up button': new AndroidIdSelector('fragment_landing_bn_sign_up'),
	    'sign in button': new AndroidIdSelector('fragment_landing_bn_sign_in')
		};
}

const viewDef: IViewDefinition = {
    android: LandingAndroid,
    gherkinName: 'landing',
};
```

---

# Pros

- Write tests at the same time we develop screen
- Good pace (at first)
- Detect bugs and regressions early

---

# Cons

- Adaptation to the stack
- Complex to maintain with app evolution
- Time consuming

---

# Maestro :musical_keyboard:

---

# Maestro

- Created in 2022 by mobile.dev
- *Kotlin* open source project
- Cross-platform (Android, iOS, ...)
- **Simple** to use

---

# Show me your flow!

- Flow describe a *test*
- Write in *yaml*
- Declarative and **simple** syntax
- Composable (flows can call each other)

---

# Simple commands

```yaml
- tapOn: "element.id" #tap on UI element
- assertVisible: "element.id" #check if the element is present
- inputText: "a text" #Input text with keyboard
- back #tap on back button 
```

---

# Simple structure

```yaml
- launchApp:
    appId: my.super.app.id
    clearState: true
- tapOn: my.button.id
- swipe:
    direction: DOWN
- assertVisible: user.profile.name
```

---

# Maestro Studio

---

# Maestro Studio

- No-Code UI Automation 
- Record Maestro commands directly from your app
- Inspect UI element
- Export recording directly to flow file

---

![autoplay loop fit](ressources/maestro-studio.mov)

---

[.text: alignment(center)]

[.column]

:+1:


- **Easy** to record a flow
- app interaction in *real time*
- no dependency

[.column]

:-1:


- Don't have access to *all* test commands
- Cannot update a current test

---

## Real *world* example with **Android Makers** app

---
# The test


1. Find our talk 
- open it
- check if we are the speakers
- put it in favorite
- filter talks by favorite
- check if our is present

---

![autoplay fit](ressources/maestro-demo-1080p.mov)

---

```yaml
- scrollUntilVisible:
    element: "Become a Maestro of Mobile Testing in 5 minutes"
    direction: "DOWN"
- tapOn: "Become a Maestro of Mobile Testing in 5 minutes"
- assertVisible:
    text: "Jordan Dahnoun"
- assertVisible:
    text: "Romain Rivollier"
- tapOn: "Favorite"
- tapOn: "Back"
- tapOn:
    point: "81%,7%"
- tapOn:
    text: "Favorite"
    index: 1
- tapOn:
    point: "81%,7%"
- assertVisible: "Become a Maestro of Mobile Testing in 5 minutes"
```

---

## Integration in your development flow

---

## Maestro Cloud

- CI dedicated to run your flows
- Reporting
- Run only on simulators
- Integration to Github PR

---

![fit](ressources/maestro-cloud.png)

---

![fit](ressources/maestro-github.jpg)

---

## Run maestro directly on your CI 

- You setup your test environment
- very light report when flow fails (Junit report)

---

# Are we **happy**?

---

# Conclusion

- Reporting less powerfull
- young product so some bug can appear
- limited to simulator for the moment
- The best experience is tied to theirs cloud platform

---

# Conclusion

- New tests are faster to write
- Costs can be lower
- maestro product moving fast
- Reduce maintenance to zero

---

# Previous stack
![inline fill](ressources/existing-stack.png)

---

# New stack
![inline fill](ressources/maestro-stack.png)

---

#Ressources :books:

- Shift Left in Mobile Engineering: [The Shift Left in Mobile Engineering by mobile.dev](https://blog.mobile.dev/the-shift-left-in-mobile-engineering-63fdbb3e34e2)

- Maestro: [https://maestro.mobile.dev](https://maestro.mobile.dev)
- Maestro Github: [https://github.com/mobile-dev-inc/maestro](https://github.com/mobile-dev-inc/maestro)

---

# [fit] **Questions?** :raising_hand: