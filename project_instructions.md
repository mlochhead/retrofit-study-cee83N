# Chinatown Earthquake Retrofit Challenge

## **Challenge**

San Francisco's Chinatown is one of the densest neighborhoods in the country. Most of its
buildings went up quickly after the 1906 earthquake and fire. Many are seismically vulnerable, and many residents live in small apartments and single-room-occupancy (SRO) hotels. In this exercise, you will evaluate possible retrofit ordinances being considered by the City of San Francisco to improve the seismic safety of this neighborhood.  

The city is considering a **mandatory retrofit ordinance**, where owners of one type of building would have to strengthen it **at their own cost**. You have been hired to select **two candidate ordinances**, compare them, and recommend one to the mayor. The proposed retrofit ordinances would bring all buildings of a given structure type to the high-code level, thus retrofitting to the point where building performance matches modern design standards. 

As a first step, pick a primary goal for your retrofit program. Possible goals are to **protect dollars** (reduce repair costs) or **protect people** (reduce the number of residents who lose their homes). There is no single right answer, and different retrofit programs likely have different impacts on each of these metrics. A good recommendation is backed by evidence from the simulation. 

In this scenario, we are considering a version of San Francisco **before it started requiring seismic retrofits**. In other words, no buildings have been strengthened yet, so every building type is a candidate, including the ones the city later targeted.

Retrofit programs will be evaluated and compared using a magnitude 7.2 scenario earthquake on the San Andreas fault, west of the city. In Chinatown the ground shaking (peak ground acceleration, PGA) is typically around **0.25 g**.

## **Analysis**

You will use **R2D**, the SimCenter's regional simulation tool, to simulate the earthquake for the existing conditions, and under the two possible retrofit programs. R2D uses FEMA's **Hazus** models: each building's chance of Slight, Moderate, Extensive or Complete damage depends on its **structural system**, **height** and **design level**, meaning how strong the building code was when it was built (*Pre-Code*, *Low-Code*, *Moderate-Code*, *High-Code*). A **retrofit** here means strengthening a building so that it behaves like a High-Code building (equivalent to modern seismic design standards if a building was constructed today).

*This is a teaching version of Chinatown. Building locations and sizes come from a real inventory, but structure types, years, values and populations were simplified. Do not quote these numbers as facts about the real neighborhood.*


## **Input Files**

| File | Description|
|---|---|
| `chinatown_buildings_example.csv` | Building inventory, one row per building (511 buildings). Load into R2D ASD tab. |
| `San_Andreas_Mw72_filtered/` | Ground shaking for the M7.2 scenario. Load into R2D as the hazard. |
| Data explorer website | Tab 1: explore the inventory. Tab 2: set up two programs and download their inventories. Tab 3: compare R2D results. |

**Key Inventory Columns**

| Column | Meaning |
|---|---|
| `StructureType`, `HeightClass`, `DesignLevel` | Hazus building type, height class and design level |
| `YearBuilt`, `NumberOfStories`, `PlanArea` | Year built, stories, floor area per story (sq ft) |
| `OccupancyClass` | RES1 house, RES3 apartments, RES4 residential hotel (SRO), COM commercial, EDU school |
| `ReplacementCost` | Cost to rebuild the building ($) |
| `Population` | Residents who sleep there at night |
| `RetrofitCost` | Cost for the owner to retrofit to High-Code ($); 0 if already High-Code. Lower for Moderate-Code buildings, which need less work. |
| `Retrofit…` columns | What the building becomes after retrofit (used by the website's download) |

**Structural Systems**

As mentioned, the retrofit programs being compared allow for a single structural system to be retrofit. 

| Code | System | Typical building here |
|---|---|---|
| W1 | Wood light frame | Single-family houses |
| W2 | Wood frame, multi-unit | 2–4 story wood apartment buildings, some with ground-floor shops |
| URM | Unreinforced masonry | Older brick buildings, many used as SROs |
| C1 | Concrete moment frame | Concrete mixed-use, apartment and commercial buildings, 3–7 stories |
| C2 | Concrete shear wall | Concrete apartment and commercial buildings |
| S1 | Steel moment frame | Larger steel-frame commercial and mixed-use buildings |

System and age are separate: every system includes buildings from more than one era, so check how many of each
system's buildings are old enough to benefit from a retrofit.

## Instructions

1. **Explore the inventory** (website tab 1). Find out:
   - how many buildings of each system there are, and how old they are (design levels)
   - where the **money** is (replacement value) and where the **people** are (residents, crowding)
   - what a retrofit would **cost owners** for each system: in total, per building and as a percent of building value

2. **Research real programs.** Use at least two in your recommendation. For each, note what problem it addressed, which buildings it covered, what it cost and whether it worked.
   - San Francisco's **unreinforced masonry (URM) ordinance** (1990s, after the 1989 Loma Prieta earthquake)
   - San Francisco's **Mandatory Soft Story Retrofit Program** (2013) for wood-frame apartment buildings
   - **Los Angeles' 2015 ordinance** for wood and older (non-ductile) concrete buildings
   - **Steel moment-frame failures in the 1994 Northridge earthquake**; SF's Tall Buildings Safety Strategy
   - **Earthquake Brace + Bolt** (bolting houses to their foundations)
   - **SRO hotels in Chinatown**: who lives there and what happens to tenants during construction or after an earthquake

3. **Choose two candidate programs** (tab 2). Each program requires **every building of one structural system** that is not already High-Code to be retrofitted, paid for by the owners. Pick the two you think are strongest for your goal and write down why, and what you predict, **before** running R2D. Download each program's inventory from tab 2. It swaps in the `Retrofit…` columns for the covered buildings; a
   retrofitted URM building is modelled as reinforced masonry (RM1). Don't edit the original inventory.

4. **Run R2D three times** with the class settings provided by your instructor: the original inventory (baseline),
   Program A and Program B. Export each run's building results table to CSV by right clicking on the results and saying 'Save to CSV.' Name them clearly. 

5. **Compare** (tab 3). Load the three files and pick which system each program retrofitted. For each program the website reports:
   - **Savings**: repair cost avoided in this earthquake (baseline − program)
   - **Residents protected**: displaced residents avoided (baseline − program)
   - **Cost to owners**: total, per building and as a percent of building value
   - **Benefit–cost ratio** (savings ÷ cost; above 1 means it pays for itself in this earthquake), **net benefit** (savings − cost) and **cost per resident protected**

   *Displaced residents* follow the Hazus rule: residents of apartment buildings count as displaced if the building's most likely damage is Extensive (90%) or Complete (100%); single-family houses count only for Complete.

## Deliverables

Write **short memo** to the mayor comparing Program A and Program B and recommending one. You can also choose to recommend neither program if you think the baseline inventory is best; however, you should have a reason for saying so. 

**Questions your memo should answer**

- Which programs did you choose to evaluate, and why? 
- Which programs, if either, do you recommend? Why? 
- What goal were you targeting with your retrofit program (cost savings? minimize disruption to people?) Based on this goal, discuss the two potential programs and what you see as the benefits of your selected program.
- In these proposed retrofits, as with past retrofit ordinances in San Francisco, building owners pay. Is that fair, and who do you think really bears the cost (owners, tenants, the city)?
- What are the limitations of this type of analysis?