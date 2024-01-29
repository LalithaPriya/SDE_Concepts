https://medium.com/@rahulmora007/how-multiplayer-games-uses-fly-weight-pattern-to-optimize-memory-e17064395b1b

**How multiplayer games use Fly Weight Pattern to optimize memory**

When we create each object for each weapon, then for a million weapons a million of each of the above attributes will be created.

size for: \
gun type : 4B \
~ size of each image: 16 KB \
coordinates: 8B \
curr capacity: 4B \
~ size of each object = 17KB \
memory for a million objects = 17,000,000 \
Kilo bytes = 17 GB \
17GB is really huge and consuming 17GB just for weapons is just impossible for any game run.


**How can we solve this?**

If we observe, there can only be a limited type of guns, and for each gun the image, gun type, and max capacity are going to be constant. Only mutable variables are co-ordinates and current capacity. So, if we can find a way to efficiently organize the constant/immutable variables to be re-usable then we can reduce a lot of memory usage.

**What can we use to solve?**
The approach that we discussed above is what the fly weight pattern uses to solve the above issue. Flyweight pattern organizes all the immutable variables into re-usable objects which reduces the cost of memory usage.

*Terminology:*
1. Intrinsic objects are the objects which are immutable i.e., does not change with respect to the environment. Examples are gun type, image, max capacity, etc. in the above example

2. Extrinsic objects are mutable objects i.e., they change w.r.to environment. Examples are co-ordinates and current capacity.

3. Flyweights are the objects which are created once and are re-used again.

4. FlyweightFactory is the container/object which stores the flyweights in a cache and returns the fly weight object when requested.

Working:

Whenever the game needs to create a Weapon, based on the weapon type mentioned a weapon type(fly weight)object which has all intrinsic objects is first checked is cache if it present and create an object and stores it in cache if not present and returns the stored object to the Weapon. Thus, each weapon type is being created only once and is being re-used multiple times.

Cost of memory consumption: \
For each GunType = 4B+16KB+4B =~ 17KB \
For Each Gun: \
co-ordinates: 8 Bytes \
currCapacity: 4 Bytes \
Total for each gun: 12 Bytes \
If there are 1,000,000 guns = 12,000,000  \ 
Bytes = 11.4 MB \
If there are 2 types of guns, then total memory will be = 11.4MB + 34KB

