# Tutorial: UPS Optimization

## NOTE:

This article is intended to show users how to generally change their factory designs to make their bases more performant.
For figuring out what specific components of your base are consuming more time than they should, see [Diagnosing Performance Issues](https://wiki.factorio.com/Tutorial:Diagnosing_performance_issues).

## Definition

**Updates Per Second** (abbreviated UPS) is the measurement of frequency that Factorio's simulation runs at, which can be viewed by selecting the `show-fps` option in [debug mode](https://wiki.factorio.com/Debug_mode). By default, Factorio will try to run the game's simulation at a rate of 60 times per second. Having a UPS less than 60 means that the save is unable to simulate the game fast enough, which is a common problem when creating large, hardware-demanding factories.

**UPS Optimization** is the process of re/designing Factorio bases to try to be as hardware efficient as possible, usually to push the factory's scale to it's utmost limit. Even if not pushing for the largest production rate possible for a given computer, knowing the underlying computational cost between different game entities and interactions can help stave off or even prevent the onset of performance issues with large bases or on systems with weaker hardware.

## Limitations of this Article

This article is not intended to be a prescriptive tutorial on how you should build your factory. UPS efficiency is simply another factor to optimize your designs around, similar to speed, space efficiency, resource cost, power consumption, simplicity, robustness, beauty, and so on. The content provided here is simply to illustrate how to build the most UPS efficient factory possible; whether or not you abide by these rules (or which rules you choose to abide by) are ultimately up to the player. Playing with biters on will always be less UPS efficient than playing with biters off, but that doesn't mean you can't play with biters if you want, and it also doesn't mean you can't improve your UPS via other means.

This article is not intended to provide advice for the average playthrough, because as long as your computer meets Factorio's minimum specs, the average Factorio playthrough has no need for performance optimizations. Factorio's mechanics are already highly optimized, and it is exceedingly rare for performance issues to arise before launching the first rocket. The content in this article is instead directed at users who wish to [megabase](https://wiki.factorio.com/Glossary#M), play large overhaul modpacks where the average base size is significantly larger than vanilla, or are running Factorio on hardware which lies below Factorio's recommended minimum.

This article is intended to be a general summary of all of the information and testing recorded and aggregated thus far related to keeping UPS as high as possible. **It is not (necessarily) a list of items that, if you fix, will make your game run better.** The UPS of a build or base is not a uniform measurement of a particular build's hardware efficiency, since there are many factors which influence UPS. If Build A has a higher UPS than Build B, then:

* Build A could truly be more hardware optimized than build B.
* Build A could be running on a machine with better hardware (CPU, RAM) than build B.
* Build A could be running on a different operating system than build B.
* Build A could be running on a different (perhaps more modern) version of Factorio than build B.
* Build B might have other applications running in the background while build A does not.
* Build A and Build B might not be performing equivalent tasks, or the method of comparing them is malformed in some way.

When concerned with the task of optimizing ones base to be more performant, these external factors must be controlled against in order to gain a reasonable confidence in the difference of performance between two designs. Check time usage statistics in the debug menu to help determine what types of entities in your build are consuming disproportionally more time than others.

This article uses numerous sources to assert its claims, all of which have been benchmarked to test their validity. While these tests are rigorous, they may also be out of date if they were performed on an older version of Factorio. Current or future Factorio versions may invalidate the advice given here, or it may not; the only reliable way to be sure is to create a well designed benchmark and run it yourself. For a tutorial on how to properly create design benchmarks, see [here](https://www.reddit.com/r/technicalfactorio/comments/lxidhz/guide_how_to_benchmark_in_factorio/).

Finally, this article only claims to apply to vanilla Factorio. Many of the UPS optimization strategies listed here will apply to modded playthroughs just as well, but because of the sheer number of possible mod configurations and the variety of their behaviors, this article cannot reasonably hope to assert that the advice given here is applicable in even most cases. Again, your best bet if looking for UPS optimization advice on modded playthroughs is to search their respective communities, ask the mod authors themselves, or, failing that, create benchmarks yourself and make the results publicly available.

## Performance List

Below is a list of the most important factors to UPS performance for a typical Factorio playthrough, ordered from most impactful to least impactful on final UPS. For best results, players should typically prefer remedying items higher on this list first before ones lower down. In each section, potential solutions are provided for each section, listed from most to least effective at improving UPS.

### 1. Usage of Modules and Beacons

The more that a Factorio save has to simulate, the slower the game save will be. Therefore, the most important step to making an efficient base is to *perform as few operations as possible to achieve your ultimate production goal.* If you can get equivalent production out of fewer machines with fewer logistical steps, then your UPS will almost always improve.

Towards this goal then, high-tier productivity modules become essential. With them, you need less input resources going into your factory to reach the same output production rate, reducing not only the resource cost itself but also the performance penalty caused by item logistics. And because productivity modules can be placed in multiple consecutive stages of a factory, their effect is multiplicative over the course of a production chain.

Because productivity modules on their own slow machines down, beaconing your machines with high-tier speed modules becomes the next highest priority. This entirely counteracts the slowdown of productivity, and allows you to now also use less machines overall for the same target production, reducing overall base size and complexity, which is evidently beneficial for UPS. However, try to use as few beacons as possible while still maintaining maximum production; additional, unnecessary beacons do consume UPS themselves. The most optimal UPS designs have maximum beacon overlap, so that each beacon is touching as many assembling machines as possible.

By extension, quality itself is another modifier towards this goal, as high quality machines and modules with give even higher ratios if input material to output material. A legendary assembler filled with legendary productivity modules, surrounded by legendary beacons with legendary speed modules, has the highest production rate (and thus UPS potential) possible.

(TODO: an example showing the ratio between non-moduled base size and moduled base size. Give a count of assemblers needed to produce x items per second without modules + beacons compared to a build that does; what percentage bigger/more items needed is the non module build by comparison?)

#### Solutions

* Always use the highest tier and quality production machines (assembling machines, oil refineries, chemical plants, etc.).
* Always prefer the highest tier and quality productivity modules inside of machines wherever possible, defaulting to speed modules otherwise, and potentially efficiency modules in select circumstances (such as when trying to reduce pollution on biter heavy maps; see next section). 
* Use beacons with the highest tier and quality speed modules, and try to overlap each beacon with as many machines as possible, since beacons themselves have a UPS cost of their own.

### 2. Biters and Pollution

Due to their expensive pathfinding, collision checking, and total count typically being measured in the thousands, Biters (and AI forces in general) are the typically the most expensive component of a vanilla factory when reaching megabase scale. It is very common for even normal size bases to slow down when performing large artillery barrages on many thousands of biter nests, but even idle biters not sending attack groups can result in the largest proportional UPS drain of a typical base.

Pollution, on it's own, does not lower UPS by much at all, even at megabase scale. What pollution does do is aggravate biters which come into contact with it, causing them to form large attack groups with expensive pathfinding. Furthermore, pollution will generate new chunks with which it comes into contact with, which typically also have more biter nests which will become aggravated.

For players who are on an existing vanilla save or want to play with biters on, the best option to remain as high a UPS as possible is to leave as few biters on the map as possible. This will decrease their effect on UPS proportionally, and it will decrease the chances of your pollution cloud touching enemy nests and triggering attacks. Keeping your pollution cloud under control using efficiency modules can also be important, particularly when the pollution cloud would be generating new uncharted chunks and thus generating new nests. However, if biter expansion is on, then having a small pollution cloud will only delay biters from attempting to expand into it, so it is not a permanent solution.

It is possible to remove all biters completely from a vanilla save without cheating, but it requires a lot of set up in order to perform and poses some restrictions on the players in the map. See [here](TODO) for more details.

For players intending to build the most UPS efficient bases possible, playing entirely without biters is the most optimal. If playing vanilla Factorio where pollution as a mechanic is only used in conjunction with biters, you can also safely turn off pollution in order to save a small margin more of UPS.

#### Solutions

* Play without biters (and pollution, if not necessary).
* Remove all biters on the map, or as many as can reasonably be expected.
* Keep your pollution cloud down to avoid populating new chunks, and to prevent biter aggravation and attack parties.

### 3. Inserters

Inserters are the most UPS costly component of Factorio's logistical puzzle, not strictly because of their individual cost, but because they are so ubiquitous in every base. Moving items in and out of assemblers, trains, chests, silos, and any other building is almost exclusively performed by inserters. In addition to their frequency of use, inserters have complex movement, activation behaviors, and conditions, making them more expensive to simulate than some other Factorio entities. As a result, the most UPS optimal bases reduce the number of necessary inserters as much as possible, or more specifically, *the amount of time inserters are active* as much as possible.

Inserters are considered "active" when they are moving items from one location to another. An inserter is considered "inactive" or "sleeping" only if it has no current job. For example, an inserter that has picked up items and is holding them over a chest that won't accept them is still active, even though it's not swinging.

#### Inserter Count

Consider the following example, which is a breakdown of item transfers in a "City Block" base (pictured top) and a Direct Insertion setup (pictured bottom):

![img](https://raw.githubusercontent.com/flameSla/Factorio-The-impact-of-city-blocks-on-UPS/main/img/pic1.png)

The difference between the two is stark. Notice that even though the City Block design is much larger, the actual number of production machines (drills, furnaces, assemblers) are identical between the two designs; 90% of the additional space is just for train loading/unloading and the belt balancers. On the top, ore is mined onto a belt, which is then put onto a train, which is then taken out of the train and put onto another belt, which is then put into an electric furnace. On the bottom, ore is mined onto a belt, which is then put into an electric furnace. The bottom design does the exact same thing as the top, but with fewer inserters, over a smaller area, and eliminates the cost of train transport entirely.

Note also that the city block design uses fast inserters rather than bulk inserters, meaning that the fast inserter will have to swing more times (and remain active for longer) to move the same amount of items as the bulk inserter. Because the vast majority of an inserters UPS cost is during it's swing, using inserters with large stack sizes are almost always better than inserters with smaller ones. The most UPS efficient bases are ones in which inserters are swinging the least amount possible.

It should be noted that the example above is a contrived example, purely for illustration. City-block designs are useful for their modularity and ease of expansion, but because of their overreliance on item transfers between logistics types they're far from UPS optimal. A city-block base that uses all other tricks and best-practiced defined on this article will *never* be more UPS optimized than a base that uses a simpler method of logistics, due to how important the efficiency of item transport is for the final UPS of a base.

#### Backpressure

Direct insertion is also particular UPS efficient in combination with something called "backpressure", or the idea that certain factories need to wait for a machine to work.

"Back pressure is when supply always exceeds demand so that when an inserter picks stuff up it always gets max items"

#### Inserter Clocking

Sometimes, backpressure cannot be achieved by overproduction of previous steps, particularly when crafting times for particular items are especially long. The best example of this is steel smelting, which requires huge amounts of smelters with a slow crafting speed. It's very rare to get backpressure here, and inserters left to their own devices will swing once for every steel plate, instead of once for every 12 steel plate.

However, we can coerce inserters to behave as we want.

Adding a clock circuit to trigger inserters at appropriate intervals does incur an additional UPS cost, even when designed correctly to minimize it's effect. However, when used properly in the correct application, this additional should be less than the amount of UPS saved by the reduction of inserter swings. 

Not all production steps benefit from inserter clocking.

#### Solutions

* Design/redesign your base around reducing the number of inserter swings. Direct Insertion between machines is king - it is the most simple way to take the output of one machine and put it into another. 
* If you don't want to use DI, avoid moving items between logistics types. If you want to use belts, use *only* belts; if you want to use trains, use *only* trains. Avoid moving items from trains onto belts, or from belts onto trains; doing this is essentially redundant. You can use bots as well, but read their section below for caveats.
* Prefer using stack/bulk inserters instead of regular, fast, or long-handed inserters *if* it will reduce the total number of swings that will occur between machines.
* [Inserter clocking](https://www.reddit.com/r/technicalfactorio/comments/ju2ngg/inserter_clocking_tutorial/) can be a way to ensure the total number of inserter swings kept as few as possible (and thus the active time of inserters as low as possible).
* Because inserters are the most important design constraint in regards to a base's final UPS, many of the subsequent optimization strategies in subsequent sections will be entirely just to reduce the amount of time inserters are active.

### 4. Fluid Networks

(TODO. This subject will likely change a lot with the new fluid mechanics. However, the rule of having as few fluid carrying entities as possible will likely still hold true.)

#### Solutions

* Use as few fluid network entities as possible.
* Producing fluid on-site (particularly water with offshore pumps) is almost always better than attempting to transport it over any distance.

### 5. Power Generation

The most UPS efficient method for generating power is with solar panels and accumulators, and by a wide margin. Factorio is able to optimize the solar panels and accumulators together into one massive entity, whereupon it calculates power generated in constant time as `brightness of sun * power output of solar panel * number of solar panels`. Accumulators are similarly optimized, since they trend towards having the same charge and discharge cycles naturally some time after being placed, meaning that as time progresses the complexity of accumulator calculations is also `O(1)`. The only drawback to using solar panels in a factory is the massive amount of space and time that they require to generate enough power for large bases, but this is a gameplay consideration, not a UPS one.

Reactors, by comparison, are much more involved. They have both heat and fluid networks which are both complex and expensive to simulate. For perspective, the time cost of just the reactors themselves is the sum of 4 different entity categories (`Boiler`,`Reactor`,`Heat Manager`, and `Generator`), whereas solar and accumulators only get one apiece. In addition, reactors need a whole suite of supporting infrastructure to remain operational; uranium miners, sulfuric acid production, centrifuges, fuel assemblers, waste processing, and of course the logistics to transport all the items and fluids necessary to support this production chain. Solar panels have no such runtime requirements once they're constructed, and thus no additional UPS cost whatsoever.

Any power setup that boils steam for power will almost certainly be more complex to run and thus less UPS performant than solar panels. However, among said boiler setups, the ones with the highest energy density are always the best option for UPS, as they require the fewest number of entities to produce a particular power demand, reducing their simulation complexity and the infrastructure needed to support them. This means that fusion reactors are better than nuclear reactors, and that both of those are far better than steam engines.

(TODO: a comparison of heat networks. This will likely change in 2.0 with the advent of fusion reactors, though it's unlikely that they will ultimately trump solar panels at the extreme.)

(TODO: However, due to their large space requirements, solar panels are suboptimal for power generation on a [Space Platform](TODO). In this circumstance, you're better off going with fusion reactors.)

#### Solutions

* Use solar panels and accumulators for power generation, if possible.
* If you cannot/do not want to use solar panels, then power setups with the highest energy density should always be preferred.
* If you cannot/do not want to use solar panels, keep your boiler setups (of whatever kind) as simple as possible. Avoid using more heat pipes on nuclear reactors than necessary. Avoid storing water or steam in tanks, or sending them through elaborate pipe networks prior to discharging them through turbines.

### 6. Electric Networks

TODO: rephrase
When a base has excess power production, Factorio only has to calculate the corresponding energy drain of all connected electrical entities, as the active speed of all entities is capped to their maximum. However, when power supply dips even slightly below complete satisfaction, the game now has to calculate the new speed for *every* single connected entity per tick. This additional cost usually comes in the form of a large lag spike that appears whenever power dips below minimum satisfaction. Avoid this to ensure smooth performance.

Expanding/merging/separating power networks are relatively expensive operations, though typically they only happen during construction instead of during a base's operation. The one exception to this is [Power Switches](https://wiki.factorio.com/Power_switch), which dynamically connect and disconnect electrical networks based on some logistic or circuit condition. Frequently doing this on very large networks will start to incur a noticeable performance cost. If using a power switch for an emergency power setup and your circuit "thrashes" (quickly enables and disables itself when approaching it's configured threshold) then consider creating a [latch](https://wiki.factorio.com/Tutorial:Circuit_network_cookbook#Latches) to govern it instead.

Electric networks in Factorio are not multithreaded [[1]](https://mulark.github.io/tests/test-000013/test-000013.html), which means all entity energy drain and production calculations have to be done per entity per electric network they are a part of. In most Factorio bases, the entire base lies on one single connected electric network, so this is imperceptible. However, bases with very many (>100) isolated electric networks can start to incur a noticeable performance cost, and if such networks are superfluous, offer a quick avenue for optimization.

#### Solutions

* Ensure that the base always has a surplus of power production, such that brownouts and blackouts never occur (or occur as infrequently as possible).
* Avoid using power switches to dynamically combine and separate electric networks, where possible. If they must exist, reduce the frequency in which it is triggered.
* Combine many small electric energy networks into one large one, whenever possible. Remove any unnecessary isolated electric networks where they occur.
* If two separate electric networks must exist, reduce the number of entities that lie in both networks at the same time. Entities that do this have to share their power demand and consumption, meaning that they are processed `N` times for the `N` networks they overlap.

### 7. Bot Networks

Between the "primary" logistics options (belts, trains, and bots) bots are the worst option for bulk transport, which is almost all of the logistics of a large scale base. Bots excel in constructing small quantities of complex items and delivering items to players, but for large scale transport their tiny relative cargo size means the quantity of bots required is exceedingly high, even with many bot-speed technologies researched. The only vanilla recipe for which it has been shown that bots are at least as good as the other logistical options is when delivering satellites to rocket silos, due to the very low throughput required.

If bots are desired regardless, reduce bot network footprint as much as possible, in order to reduce the total distanced traveled between robots. This is desirable outside of UPS anyway, as it reduces energy consumption and requires less recharging, resulting in both fewer roboports and fewer robots in flight.

#### Solutions

* Avoid using logistics bots to transport bulk items entirely, preferring belts or trains.
* Avoid having large robot networks. Robot cost is directly proportional to the amount of time spent flying from point to point. Reducing the distance between destinations not only reduces the amount of time robots spend flying (and thus their energy use), but it also reduces the total amount of robots you need active to supply a given transfer rate, both of which improves UPS. [[1]](https://mulark.github.io/tests/test-000201/test-000201.html)
* Remove legacy roboports that are no longer used at all, *as empty, idle roboports do still consume UPS*. A good example of this is that players will typically build roboports into their solar arrays to allow them to be automatically constructed, but will neglect to remove the roboports once the array is fully constructed and robots are no longer need to travel there.

### Trains

At megabase scale, trains themselves can also be a considerable UPS cost. Trains need to pathfind through the rail network, which is likely large and interconnected, providing many possible avenues to the destination which have to be compared. Further, trains perform collision checks at all times, and so they always have some overhead when they are moving from station to station. These collision checks are performed per wagon, meaning that the overall size of the train influences it's UPS cost, not just the amount of different trains pathfinding through the network. Trains with more wait conditions per stop also perform worse on average than trains with less wait conditions per stop.

Different categories of train stop conditions themselves also incur different UPS costs. [[1]](https://mulark.github.io/tests/test-000047/test-000047.html) Conditions such as "Time Passed" and "Inactivity" are much cheaper for the game to calculate when compared to conditions like "Item Count". If you have a very high amount train schedule stops which use a UPS expensive condition, switching to a cheaper equivalent condition across the board might yield a noticeable UPS improvement when the number of trains with said schedule is high.

Even if complex schedule conditions like "Item Count" are absolutely necessary, it may still be possible to reduce their UPS impact (under certain circumstances). For example, suppose you need to check a complex assortment of items at a particular station, but you know that it will take at least 3 minutes before the stop can reasonably be expected to  load those items. What you can do in this case is prepend a comparitively cheap "Time Passed" condition, ANDed with the rest of your wait conditions:

![img](example)

Factorio implements [short-circuiting](https://en.wikipedia.org/wiki/Short-circuit_evaluation) with wait conditions, which means that the game will check "Time Passed" first, and will only evaluate the following expensive checks if the first condition is true. Hence, instead of checking the set of expensive conditions every single tick while the train is stopped at that station, if the conditions are met by the time 3 minutes have passed the game will only have to check the expensive conditions exactly once. [[2]](https://mulark.github.io/tests/test-000030/test-000030.html)

#### Solutions

* Reduce the number of moving rolling stock in your rail network. This can be achieved by either reducing the amount of trains in the network, reducing the size of each train in the network, or both.
* Fewer, larger trains cost less UPS on average than many, smaller trains. [[3]](https://mulark.github.io/tests/test-000104/test-000104.html)
* Increase the speed with which trains navigate your rail network. The less time trains are pathing on rails, the less impact they will have on your final UPS. [[4]](https://mulark.github.io/tests/test-000106/test-000106.html) This can be achieved by using the highest acceleration fuel available and by using train layouts with higher locomotive to wagon ratios.
* Simplify your rail networks. Avoid a single connected network with very many paths, in favor of smaller separate networks with only one or two paths. Not only will this reduce pathfinding time (if such a cost was large) but having more dedicated routes for each train will likely reduce the impact of train intersections and decrease train travel time, a compounding positive effect on UPS.
* Avoid long sections of diagonal rails where possible, preferring straight rails instead. Trains travelling on diagonal rails incur more collision checks than trains travelling on straight rails. There also seems some evidence to avoid placing rails over ore patches, but this effect is much more minimal. [[5]](https://mulark.github.io/tests/test-000051/test-000051.html)
* If your base contains train schedules with very many stops, prefer wait conditions like "Time Passed", "Inactivity", or "Circuit Condition". Avoid using "Item Count", as that is the worst performing condition by far. If you need to have a complex train set of conditions for a particular stop, consider prepending the condition with "Time Passed AND ..." to reduce the amount of time spent on those expensive checks. 

### Splitters

Firstly and most simply, avoid the use of splitters if possible. Splitters are rarely actually necessary, depending on the design goals. Consider a simple belt example, where 4 fully saturated blue belts of iron plates are sent to 4 steel smelting columns:

![example showing balanced](TODO)
![example optimized for UPS efficiency](TODO)

Here, the balancer in the middle is completely unnecessary. Each origin column produces 1 blue belt of iron plates, and each destination column consumes 1 full belt of iron plates; assuming that the inputs to the system remain similarly balanced (which they should be under ideal conditions) then the output will also remain perfectly balanced naturally. Consider another example with ore mining:

![example showing balanced](TODO)
![example optimized for UPS efficiency](TODO)

Here


### Belts

Most of the optimization techniques around belts are closely related to inserter mechanics; this section will reference portions of the above material.

Prefer using the highest tier belt whenever possible. The slower the belt, the longer it takes for an inserter to pick up items, meaning that the inserter remains active for longer than necessary.



It is commonly believed that keeping belts compressed is beneficial for UPS - but while this may have been true for versions of Factorio before 1.0, it is [no longer the case](TODO). There is no meaningful difference in UPS between a partially compressed belt or a fully compressed belt. Similar myths about underground belts being more UPS performant than regular ones have also been disproved on modern Factorio versions. On their own, there is no noticable difference between belt compression levels.

*However*, if a suboptimal belt saturation keeps inserters awake for longer than necessary, then this will have a far greater negative effect on UPS than belt compression.

Keeping belts compressed is beneficial for UPS, though likely not in the way that you expect.


**


[Since 0.16](https://www.factorio.com/blog/post/fff-176), belt mechanics changed to follow an optimized simulation scheme which is much better than naively moving every item on every belt simultaneously. While this system is definitely more performant than before, it's complexity makes optimizing belts for UPS a significantly more involved task, and requires at least a basic knowledge of how belts work internally. 


The final component for optimizing a factory's belts requires a least a basic knowledge of how belts are simulated internally. For a more complete and robust description on how modern belts operate, see this [article written by smurphy1](https://www.reddit.com/r/technicalfactorio/comments/r6ye86/mechanics_of_transport_line_splits/). Summarized simply:

- Items on belts follow what are termed "transport lines". Transport lines are typically several tiles long, but "break" (split) under certain circumstances to keep individual transport lines within a manageable set of lengths.
- You can view transport lines using the `show-transport-line` debug option. The lines have arrows indicating their direction, and are color coded based on their state.
- Transport line breaks are always created by splitters, underground belts, a change in belt speed (blue belt to red belt, for example), or a circuit or logistics condition which can stop the belt from moving. In addition, a transport line is always split if it is more than 200 tiles long.
- Transport line breaks can be dynamically caused by inserters picking up or putting down items onto a belt and during sideloading. After certain periods of inactivity, these dynamic line breaks can be joined back into one large one, known as "remerging".
- The dynamic splitting and remerging of transport lines caused by inserters and sideloads is comparatively expensive.
- Placing upstream inserters close to transport line breaks (less than 3 tiles away) avoids creating a new break, avoiding the expensive splitting and remerge logic mentioned above. Additionally, the closer the inserter is placed to the break, the less amount of time the game has to "search" that transport line to find the items it wants. By using underground belts, you can specify a transport line break in a particular spot to take advantage of these properties.
- Even better performance can be achieved by having multiple inserters share the same transport line segment. This reduces the total number of transport lines along a belt that the game has to simulate, which offers slightly better results than forcing a new line break as close to each inserter as possible.

It should be mentioned however that the belt optimization techniques mentioned here are very minute in effect, and very complex to do properly. Highly wasteful transport line management will have an almost imperceptible cost for the average megabase, let alone a regular playthrough. Such techniques are only typically employed when every single margin of performance is necessary.

#### Solutions

* Always use the fastest belt speed possible, as the faster the belt, the quicker an inserter can pick up it's stack size worth of items, reducing the amount of time that inserter is active.
* Avoid using splitters, if possible. If you need a certain amount of items on a belt, then put exactly those items on the belt in the first place. Most balancing operations can be substituted with overproduction and sideloading, which have additional positive UPS effect. Train car balancing can also be similarly prevented by keeping input lines balanced from the get-go.
* When picking up items from a belt, prefer having inserters pick up only from one side of the belt; picking up from both sides at the same time slows them down, keeps them active for longer, and reduces UPS. This can be achieved by either putting 2 different items on either lane, or by only using one lane of the entire belt.
* When picking up items from a belt, try to ensure that the belt lane that the inserter is picking up from is fully compressed. This allows the inserter to grab the contents of the belt as quickly as possible, reducing active time. This can be achieved by slightly underbuilding a production block to use slightly less than one belt
* If you want to use a full belt of a single item as input, [use a sideload halfway down to keep an inserter's preferred lane compressed](https://www.reddit.com/r/technicalfactorio/comments/nwu7ky/ups_efficient_double_sided_belts_same_item_on/).
* When designing your production blocks, try to have as few transport lines as possible, by reducing the amount of splitters and circuit controlled belts, where possible. Manipulate where exactly transport line breaks are placed to have them close to your inserters to reduce search time. Try to put as many inserters as close to an existing break as possible to prevent dynamic splitting and remerging of transport lines.

## Other Potential Causes of Lowered UPS

### Mods

Mods (particularly those with expensive per-tick updates) are a big potential reason why an otherwise UPS optimal base might be performing more poorly than expected.

(TODO: needs expansion)

### Radars

Because radars constantly attempt to chart new chunks, having very many radars (>1000) can start to have a negative influence on UPS. Once an area within it's range is charted, consider replacing interior radars for ones further out on your base's perimeter, or simply reducing/removing them altogether.

If live base coverage is all you're looking for out of radars, consider the [VisionRadar mod](https://mods.factorio.com/mod/VisionRadar?from=search), which adds a radar which has no chunk scanning functionality (and thus very little UPS impact) but has a larger vision radius.

### Circuit Networks (In Massive Cases)

Circuit network cost per game tick can be roughly intuited as:
    
* `the number of signals changing on a network` *
* `the frequency of which those signals change on a network` *
* `the amount of connected entities influenced by these changes` *
* `the number of active circuit networks in the save`.

Having
Having a disproportionately large amount of any of these categories (or all in conjunction) will likely see a performance cost. It is better to send a single signal for 1 tick as opposed to every tick, and it's bette

(TODO: needs expansion)
