### **Desfer canvis a Git**

A Git, hi ha diverses maneres de desfer canvis, depenent de la situació específica. Aquí tens un desglose dels comandaments més comuns i quan utilitzar-los:

---

### **1\. Desfer canvis no afegits a l'àrea de preparació (staging area)**

Si has modificat fitxers però no has fet `git add`, pots desfer els canvis amb:

```bash
git restore <fitxer>
```

Per desfer canvis en tots els fitxers modificats:

```bash
git restore .
```

Això restaurarà els fitxers a l'estat del darrer commit.

---

### **2\. Desfer canvis en l'àrea de preparació (staging)**

Si ja has utilitzat `git add` però encara no has fet `git commit`, pots treure els fitxers de l'àrea de preparació sense perdre els canvis realitzats:

```bash
git restore --staged <fitxer>
```

Per treure tots els fitxers del staging:

```bash
git restore --staged .
```

---

### **3\. Desfer l'últim commit (mantenint els canvis)**

Si ja has fet un commit però vols desfer-lo i mantenir els canvis en el directori de treball:

```bash
git reset --soft HEAD~1
```

---

### **4\. Desfer l'últim commit (eliminant els canvis)**

Si ja has fet un commit i vols desfer-lo eliminant completament els canvis:

```bash
git reset --hard HEAD~1
```

⚠️ **Advertència:** Això elimina permanentment els canvis. Utilitza'l amb cura.

---

### **5\. Desfer canvis en un fitxer específic al seu estat d'un commit anterior**

Per restaurar un fitxer a un commit anterior sense afectar altres canvis:

```bash
git checkout --source=<commit_hash> <fitxer>
```
⚠️ Tin en compte que `git checkout` per a restaurar fitxers es més antic. L'alternativa moderna és usar `git restore`:

```bash
git restore --source=<commit_hash> <fitxer>
```
---

### **6\. Revertir un commit ja enviat (revert)**

Si necessites desfer un commit ja enviat a un repositori remot, pots utilitzar `git revert`. Això crea un nou commit que reverteix els canvis:

```bash
git revert <commit_hash>
```

---

### **7\. Forçar la sincronització amb el repositori remot**

Si vols desfer els teus canvis locals perquè coincideixin amb l'estat remot:

```bash
git fetch origin
git reset --hard origin/<branca>
```

---

### **Resum de precaucions**

1. Revisa sempre els teus canvis amb `git status` i fes una còpia de seguretat si no estàs segur.
2. Utilitza `--soft` o `--mixed` per evitar perdre feina accidentalment.
3. Per desfer canvis en un repositori compartit, és millor utilitzar `revert` en lloc de `reset`.

---

### **Exemples detallats**

### **1\. Desfer canvis no afegits a l'àrea de preparació**

**Situació:** Has modificat un fitxer, però no estàs satisfet amb els canvis i vols tornar al seu estat del darrer commit.

**Ordre:**

```bash
git restore <fitxer>
```

##### **Exemple:**

1. Modifiques un fitxer `fitxer.txt`.
2. Per verificar els canvis:
   ```bash
   git status
   ```
   Sortida:
   ```yaml
   Changes not staged for commit:
     modified: fitxer.txt
   ```
3. Per desfer aquests canvis:
   ```bash
   git restore fitxer.txt
   ```
   Ara el fitxer torna a l'estat del darrer commit.

Si vols desfer tots els canvis no guardats:

```bash
git restore .
```

---

### **2\. Desfer canvis en l'àrea de preparació**

**Situació:** Has fet `git add`, però t'adones que no vols incloure el fitxer al commit.

**Ordre:**

```bash
git restore --staged <fitxer>
```

##### **Exemple:**

1. Modifiques `fitxer.txt` i l'afegeixes a l'àrea de preparació:
   ```bash
   git add fitxer.txt
   ```
2. Per treure'l del staging (sense perdre els canvis al directori de treball):
   ```bash
   git restore --staged fitxer.txt
   ```

---

### **3\. Desfer l'últim commit (mantenint els canvis)**

**Situació:** Has fet un commit, però et dones compte d'un error.

**Ordre:**

```bash
git reset --soft HEAD~1
```

#### **Exemple:**

1. Fem un commit:
   ```bash
   git commit -m "Commit incorrecte"
   ```
2. Per a desfer-lo:
   ```bash
   git reset --soft HEAD~1
   ```
3. El commit s'ha desfet, pero els canvis segueixen a l'staging area. Pots editar els fitxers o fer un nou commit.

---

### **4\. Desfer l'últim commit (eliminant els canvis)**

**Situació:** Has fet un commit però vols eliminar completament els canvis.

**Ordre:**

```bash
git reset --hard HEAD~1
```

#### **Exemple:**

1. Fem un commit:
   ```bash
   git commit -m "Commit amb errors"
   ```
2. Per a eliminar completament este commit i els canvis:
   ```bash
   git reset --hard HEAD~1
   ```
3. ⚠️ **Advertencia:** Els canvis es perdran per complet. Asegurat realment que no els necessites.

---


## Response:
### **5\. Desfer canvis en un fitxer específic al seu estat d'un commit anterior**

**Situació:** Vols restaurar un fitxer a un estat específic, però sense afectar altres fitxers del projecte.

**Ordre:**

```bash
git restore --source=<commit_hash> <fitxer>
```

#### **Exemple:**

1. Busca el hash del commit al qual vols restaurar:
   ```bash
   git log
   ```
   Sortida:
   ```sql
   commit 123abc456def
   ```
2. Restaura el fitxer:
   ```bash
   git restore --source=123abc456def fitxer.txt
   ```
3. Ara el fitxer torna a la versió específica d'aquell commit.

---

### **6\. Revertir un commit ja enviat (revert)**

**Situació:** Has fet un commit, l'has enviat al repositori remot i vols desfer-lo sense alterar l'historial.

**Ordre:**

```bash
git revert <commit_hash>
```

#### **Exemple:**

1. Troba el hash del commit a revertir:
   ```bash
   git log
   ```
   Sortida:
   ```sql
   commit 123abc456def
   ```
2. Reverteix el commit:
   ```bash
   git revert 123abc456def
   ```
3. Això crea un nou commit que reverteix els canvis realitzats en `123abc456def`.

---

### **7\. Forçar la sincronització amb el repositori remot**

**Situació:** Has fet canvis locals que no necessites i vols que el teu repositori local coincideixi exactament amb el remot.

Per sincronitzar amb la branca principal:  

**Ordres:**

```bash
git reset --hard origin/main
```  

#### **Exemple:**

1. Baixa els canvis del remot:
   ```bash
   git fetch origin
   ```
2. Sincronitza el repositori local amb la branca remota:
   ```bash
   git reset --hard origin/<branca>
   ```

⚠️ **Nota:** Els canvis locals no confirmats es perdran.

---

### **Quan utilitzar cada Ordre?**

* **`git restore`:** Per desfer canvis no preparats o de l'àrea de preparació.
* **`git reset --soft`:** Si vols desfer un commit sense perdre els canvis.
* **`git reset --hard`:** Per esborrar canvis locals de manera irreversible.
* **`git revert`:** Per desfer canvis en un historial compartit.
* **`git fetch` + `git reset --hard`:** Per alinear el repositori local amb el remot.

---

### **Explicació de `git revert`**

El Ordre `git revert` s'utilitza per desfer els canvis d'un commit **creant un nou commit** que reverteix específicament els canvis introduïts en aquell commit. Això és útil quan treballes en un repositori compartit, ja que no altera l'historial existent (a diferència de `git reset` o `git reset --hard`).  

**Característiques principals:**

1. **No elimina commits**: En lloc d'esborrar un commit, crea un nou que reverteix els seus canvis.
2. **Segur per repositoris compartits**: És ideal per revertir canvis ja enviats al repositori remot sense afectar a altres usuaris.
3. **Granularitat**: Pots revertir un commit específic sense afectar a altres commits més recents.

---

### **Sintaxis bàsica**

```bash
git revert <commit_hash>
```

---

### **Com canvia la branca després d'un `git revert`**

#### **Abans del revert**

La teva branca conté un historial amb diversos commits:

```css
A --- B --- C --- D
```

On:

* `A`, `B`, `C`, `D` són commits en ordre cronològic.
* Vols revertir el commit `C`.

#### **Després del revert**

Després d'utilitzar `git revert C`, Git crea un nou commit (`C'`) que aplica els canvis inversos al commit `C`:

```mathematica
A --- B --- C --- D --- C'
```

* `C'` és el commit revertit.
* L'historial segueix sent lineal i clar per a tots els desenvolupadors.

---

### **Exemples pràctics**

#### **Exemple 1: Revertir un commit específic**

1. Mires l'historial per identificar el commit:
   ```bash
   git log --oneline
   ```
   Salida:
   ```css
   d4f7e89 (HEAD -> main) Va afegir nova funcionalitat
   a8c9f10 Corregir errors a la validació
   9b2c6d3 Implementació inicial
   ```
2. Vols revertir el commit `a8c9f10`. Executa:
   ```bash
   git revert a8c9f10
   ```
3. Git obre un editor per confirmar el missatge del nou commit. El missatge per defecte serà:
   ```sql
   Revert "Corregir errors en la validació"

   Això reverteix el commit a8c9f10.
   ```
4. Després de confirmar, l'historial ara és:
   ```arduino
   d4f7e89 Va afegir nova funcionalitat
   a8c9f10 Corregir errors a la validació
   c5d8e34 Revertir "Corregir errors a la validació"
   9b2c6d3 Implementació inicial
   ```

---

#### **Exemple 2: Revertir múltiples commits**

1. Vols revertir els últims tres commits:
   ```bash
   git revert HEAD~3..HEAD
   ```
2. Això genera un nou commit per a cada un dels tres commits anteriors, aplicant els canvis inversos.

---

#### **Exemple 3: Revertir canvis en un repositori remot**

1. Has revertit un commit localment i necessites enviar els canvis al remot:
   ```bash
   git revert <commit_hash>
   git push origin main
   ```

---

### **Consells i casos comuns amb `git revert`**

1. **Resoldre Conflictes durant el revert:** Si el commit que vols revertir afecta àrees del codi que han canviat en altres commits, podrien aparèixer conflictes. Git et demanarà que resolguis aquests conflictes manualment abans de completar el revert.
2. **Revertir un merge commit:** Per revertir un merge commit, has d'especificar el pare del commit fusionat:
   ```bash
   git revert -m 1 <merge_commit_hash>
   ```

   * `-m 1` indica que vols mantenir el primer pare de la fusió.

---

### **Avantatges i desavantatges de `git revert`**

|**Avantatges**|**Desavantatges**|
|---|---|
|Manté l'historial intacte.|Genera commits addicionals a l'historial.|
|És segur per a repositoris compartits.|Pot ser tediós si hi ha molts commits.|
|Permet revertir canvis específics fàcilment.|Pot generar conflictes en branques complexes.|

---

Quan desitges **forçar la sincronizació del repositori remot amb el local**, esencialment estàs sobreescrivint l'estat del repositori remot amb el contingut del teu repositori local. Això pot ser útil en situacions on el remot conté canvis no deistjats, però deu utilitzar-se amb compte per a evitar esborrr treball important.

---

### **Pasos per a forçar la sincronització del remot amb el local**

#### **1\. Asegúrat d'estar en la branca correcta**

Confirma que estàs treballant en la branca que desitges sincronitzar. Per exemple, si estas en la `main`:

deprecated
```bash
git checkout main
```  

```bash
git switch main
```

---

#### **2\. Forçar el canvi en remot**

Utilitza l'opció `--force` al fer `git push`. Aquesta opció sobreescriu completament el repositori el remot amb el repositori local:

```bash
git push --force origin main
```

Aç+o farà que l'estat del repositori remot coincideixe exactament amb la teua branca local `main`.

---

### **Exemple pràctic**

Suposem que tens el següent escenari:

* El teu repositori remot (`origin/main`) té commits no desitjats que no estan al teu local.
* Vols que el remot coincideixi amb els commits i l'estat del teu repositori local.

#### **Pas 1: Verifica l'historial local**

Confirma que el teu historial local és el correcte:

```bash
git log --oneline
```

Sortida al teu local:

```sql
abcd123 (HEAD -> main) Canvis locals
efgh456 Commit anterior en local
```

El remot té:

```perl
ijkl789 Canvis remots no desitjats
abcd123 Canvis locals
efgh456 Commit anterior en local
```

#### **Pas 2: Força el push**

Executa el següent Ordre per sobrescriure el remot:

```bash
git push --force origin main
```

#### **Resultat**

El remot ara tindrà exactament el mateix historial que el teu local:

```sql
abcd123 Canvis locals
efgh456 Commit anterior en local
```

---


### **Què fa realment `--force`**

El flag `--force` instrueix a Git que ignori qualsevol desalineació entre el repositori local i el remot, sobrescrivint l'historial remot amb el del repositori local.

---

### **Precaucions al utilitzar `--force`**

1. **Perill de perdre feina remota:** Això elimina qualsevol commit al remot que no estigui al teu local. Si altres col·laboradors han fet canvis al remot, les seves contribucions es poden perdre.
2. **Comunica't amb l'equip:** Si treballes amb altres persones, avisa-les abans d'utilitzar `--force`. Això evita confusions o pèrdua de treball.

---

### **Alternativa més segura: `--force-with-lease`**

Quan treballes en un entorn compartit, és millor utilitzar `--force-with-lease` en lloc de `--force`. Aquest flag comprova que ningú hagi fet canvis al remot des de la teva última actualització (`git pull`). 

**Ordre:**

```bash
git push --force-with-lease origin <branca>
```  

Si algú ha fet canvis en remot, aquesta ordre no sobreescriurà res i t'alertarà que revises els canvis primer.

---

### **Conclusió sobre sincronitzar el remot amb el local**

Per a sobreecriure el remot en local

* Utilitza `git push --force origin <branca>` si estàs absolutament segur del que fas i vols sobrescriure el remot.
* Prefereix `git push --force-with-lease` en repositoris compartits per evitar conflictes inesperats.

---

### **Què passa amb la branca després d’un `git restore`**

El Ordre `git restore` afecta els fitxers del **directori de treball** o de l'**àrea de preparació (staging)**, segons les opcions utilitzades. **No modifica l'historial de commits** de la branca.

---

### **Escenaris comuns de `git restore` i com afecta l'estat**

#### **1\. Restaurar canvis no preparats (`git restore <fitxer>`)**

**Situació:** Has modificat un fitxer però no l'has afegit a l'àrea de preparació (`git add`).

**Què fa `git restore`:** Torna el fitxer al seu estat del darrer commit (HEAD), eliminant els canvis al directori de treball.

##### **Estat de la branca:**

La branca no canvia. Només el fitxer al directori de treball torna a coincidir amb l'últim commit.

##### **Exemple pràctic:**

1. Modifiques `fitxer.txt` (canvi no preparat).
2. Utilitzes:
   ```bash
   git restore fitxer.txt
   ```
3. El fitxer torna al seu estat original de l'ultim commit. Si fas un `git commit`, aquest fitxer no inclourà cap canvi, perque no hi ha modificacions pendents.

---

#### **2\. Restaurar fitxers del staging (`git restore --staged <fitxer>`)**

**Situació:** Has fet `git add`, però no vols que el fitxer estigui a l'area de preparació (staging). Sense perdre els canvis al directori de treball.

**Què fa `git restore --staged`:** Elimina el fitxer de l'àrea de preparació sense perdre els canvis al directori de treball.

##### **Estat de la branca:**

La branca no canvia. El fitxer segueix tenint canvis locals però ja no està a l'staging area. Si fem un `git commit`, este fitxer no s'inclourà.

##### **Exemple pràctic:**

1. Modifiques `fitxer.txt` i l'afegeixes al staging:
   ```bash
   git add fitxer.txt
   ```
2. Treus el fitxer del staging:
   ```bash
   git restore --staged fitxer.txt
   ```
3. Ara `fitxer.txt` apareix com modificat però no en l'staging area:
   ```bash
   git status
   ```

   ```yaml
   Changes not staged for commit:
     modified: fitxer.txt
   ```
4. Si fas un `git commit`, el fitxer **no formarà part del commit**.

---

#### **3\. Restaurar des d’un commit anterior (`git restore --source=<commit_hash> <fitxer>`)**

**Situació:** Vols que un fitxer específic torni a l'estat d'un commit anterior.

**Què fa `git restore --source=<commit_hash>`:** Restaura el fitxer a l'estat d'aquell commit. Els canvis es consideren nous al directori de treball o en l'staging (segons les opcions).

##### **Estat de la branca:**

La branca no canvia fins que facis un nou commit. Si fas un `git commit`, els canvis restaurats quedaran registrats com un nou commit.

##### **Exemple pràctic:**

1. Restaura `fitxer.txt` a un commit anterior:
   ```bash
   git restore --source=123abc fitxer.txt
   ```
2. El fitxer ara te el contingut del commit `123abc`. Apareix com modificat:
   ```bash
   git status
   ```
   
   ```yaml
   Changes not staged for commit:
     modified: fitxer.txt
   ```
3. Si l'afegeixes i fas un commit:
   ```bash
   git add fitxer.txt
   git commit -m "Restaura fitxer.txt al commit 123abc"
   ```
   La branca tindrà el nou commit amb els canvis restaurats.  

---

### **Què passa si fas un `git commit` després d’un `git restore`**

1. **Si no hi ha canvis pendents:**  

   * El commit no incluirà res, i Git mostrarà un missatge com:  

      ```vbnet
      On branch main
      nothing to commit, working tree clean
      ```

2. **Si hi ha canvis pendents:**  

   * Si restaurem un fitxer i despres el modifiquem, el commit inclourà els canvis restaurats o modificats, depenent del que estigui a l'àrea de preparació (`staging`).

3. **Si has restaurat des d'un commit anterior:**  

   * El nou commit reflectirà els canvis del fitxer restaurat.

---

### **Flux típic amb `git restore`**

1. Modifiques un fitxer.
2. Utilitzes `git restore` per desfer els canvis o treure’ls del staging.
3. Decideixes si cal fer un commit:
   * Si has restaurat els canvis, **no cal fer un commit.**
   * Si has restaurat des d’un commit anterior o has fet nous canvis, pots preparar-los (`git add`) i fer un commit.

---

