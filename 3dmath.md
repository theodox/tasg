@3dmath 
# 3d math for tech artists
* Good 3d knowledge is the difference between good and great in TA work
* Most of us learn by intuition and experimentation
	* formal math language is often intimidating
	* But learning how the math works will make you a much more effective TA
* Step 1: Trig
	* The first important building block is trig
	* Your probably learned this in high school and then filed away under ‘why do they make me learn this’
	* Trigonometry is ‘the science of triangles’ 
		* Not surprisingly it’s important for all sorts of reasons in 3d math!
		* In our application we don’t really need to calculate the answers - the computers will do it for us.  But we do need to know the tools because they influence a lot of things we do:
			* constructing geometry
			* rigging
			* shading
	* Basics of trig:
		* Interior angles:
			* All triangle angles sum to 180
			* know two, you know three
			* Practical application:
				* predict the angle of a rigged strut system
		* opposite angles
			* When two lines cross, the opposing angles are equal
			* Used with interior angles can find missing angles
			* Application:
				* Refraction shading
		* similar triangles
			* angles don’t very with the size of a triangle, only the proportions
			* angles of a 3:4;5 triangle are the same as those of a 6:8:10 triangle
		* Sine and Cosine
			* drove you crazy in HS, but really simple
			* Imagine a circle with a radius of 1 plotted on a grid
			* SINE = x component of the circle for a given angle
			* COSINE = y component of the same thing
			* this is way sin and cosine are 90 degrees off in phase
			*  Singly, a sin or cosine represents an angle
			*  Sine and cosine together convert an angle into a vector
				* and conversely, if you normalize the vector you can convert it into an angle
			* Angles and unit vectors are INTERCHANGEABLE in a given frame of reference — but ONLY in a given frame of reference
				* ‘a rotation of X degrees’ implies “where 0 points this way’
				* We conventionally set that to x, y with x as the cosine and y as the sine
			* You can convert a vector into a rotation - but going the other way you’ve lost the length of the vector
		* Tangent
			* Go back to the unit cirle
			* the tangent is the ratio of the y over the X
			* For a unit circle, that means it’s also the slope of the line
			* It’s infinite when X = 0 !
				* Applications
				* Atan2:
					* convert a slope into an angle
		* Sine,  Cosine and Tangent  are clamped (again, remember that unit circle).  So you can’t derive a WINDING from a sine or cosine (or, for that matter, from a vector
	* Vectors
		* We usually think of a vector as a collection of XYZ numbers, but really a vector represents an N-dimensional quantity. you can have 2d and 3d  and 10-d vectors
		* Although we use vectors to represent points, they are not the same thing!
			* A vector is a relative quantity, a point is an absolute quantity
		* The thing which distinguishes a vector from an arbitrary collection of numbers is that vectors can be added and scaled
			* collection of elements calledvectors, which may be added together andmultiplied ("scaled")
		* Vector methods work the same way regardless of dimensionality 
			* Except cross product
		* though of course higher dimensional vectors are hard to visualize. 
		* addition:
			* Add the corresponding piects:
				* (1,2,3) + (1,1,1) = (2,3,4)
		* multiplication /division (“vector’ product):
			* multiply corresponding places:
				* (1,2,3)(2,3,4) = (2, 6, 8) 
			* or divide:
				* (1,2,3)/(2,3,4) = (1/2, 2/3, 3/4)
		* size:
			* size of a vector is the length of the ‘triangle’ formed by the vector in N-space
			* so, a 2d- vector is sqrt(x^2 + y^2)
			* a 3d vector is sqrt( x^2 + y^2 + z^2)
			* 4d = sqrt (x^2 + y^2 + z^2 + w^2) 
			* … etc
			* Application:
				* distances between positions
				* convert positions into angles
					* as long as you ‘project’ onto a plane
		* A vector is ‘normalized’ if it has a size of magnitude of 1 (so sqrt(x^2 + y^2) = 1 or sqrt(x^2 + y^2 + z^2) = 1
		* dot or ‘scalar’ or ‘inner’ product:
			* Math wise:
				* multiply corresponding points and add them
				* (1,0) dot (.7, .7) = 
					*(1 *.7)  +  (0 *.7) =   
					.7
				* (1,0) dot (0, 1)  = 
					(1 * 0) + (0 * 1) =   
					0
				* (-1,0) dot (1,0) =   
					(-1) + (0) = 
					-1
			* The projection of one vector onto another
				* that’s why a dot of zero = a right able
				* a dot of 1 = parallel angles
				* a dot of -1 = opposite angles
			* Applications:
				* Fresnel -style ‘how big is this angle’ measurements
		* cross product:
			* math wise:
				* (1,0,0) x (0,1,0) = (0,0,1)
				* What’s the algo here?
			* Cross of two 3d vectors is at right angles to both
			*  The result's magnitude is equal to the magnitudes of the two inputs multiplied together and then multiplied by the sine of the angle between the inputs.
			* the direction of the vector is _arbitrary_ - it’s a convention, not a mathematical property.  
				* Left hand and right hand options: equal but opposite.
				* Max is LH, Maya is RH, DX is ?? OGL is ?? 
			* Useful for lots of things:
				* rigging
				* attaching objects
		* * Vector tricks:
			* revers a vector: multiply by -1
			* project a vector:
				* Truncate: gives you the projection
				* Truncate and renormaliza if you need a normalized vector
					* e.g.: angle to character pos from ground origin:
						* character root = [1,2,10]()
						* flatten = [1,2]()
						* normaalize = 
				* Or multiply by zero in the flattened field:  e.g. project onto XY plane with  my vector * (1,1,0)
			* Normalize a vector:
				* divide by its own length
				* When you know a vector is normalized, you get all the trigonometric properties for free
				* if you don’t normalize, your results will be scaled up or down by the magnitude of the vector
				* rule of thumb: always normalize vectors before doing angle work, don’t normalize for position work.
		* Radians
			* more common in math than degrees
			* expresses distance around the perimeter of our unit circle
			* Pi is the ratio between a Unit circle and a unit square:
			* perimeter of a unit circle = 3.1417…
			* perimeter of a circle with a unit RADIUS = two pi
			* so pi radians = 180 degrees
			* two pi radians = 90
			* etc
				* A radian is about 57 degrees
			* radians are useful for hand math
				* but also for turning angles into distance-around-circle:
				*  the straight line distance from (1,0) to (0,1) is about 1.41
				* the arc distance is pi/2 = 1.57
			* Radians to degrees = Rad * 57.xxx*
			* degrees to radians = deg / 57.xxxx
	* Matrices
		* so far we’ve only considered a couple of things you can do to vectors
			* Scale
			* Add
		* You can also rotate them:
			* here’s an example in 2d, which goes back to our unit circle.
			* I’d like to rotate my vector (1,0) by 45 degrees.
			* We remember that 45 degree rotation is (.707, .707)
			* How do we apply that to a vector ?
				* we know the result is the same as subtracting .293 from the first component and  adding .707 to the second component
				* But if you use add that vector multiple times you don’t get a rotation
				* We really doing two things here
					* scaling down the X component by the sin of 45
					* Adding the cosine of 45 to the second component
				* how to do this in a single operation? 
				* You can write this as a matrix….
					* (.707, .707)
					* (.707, -.707)
			*  When you multiply a vector by a matrix, you’re essentially taking each component of the vector and taking the dot product with each column of the matrix
				* need a note here about rows and columns: most texts are column-major, but graphics is usually row-major
			* Each vector \> column dot product becomes a component of a new vector
				* here we get:
				* (1,0) dot (.707, .707) = .707
				* (1,0) dot (.707, -.707) = .707
				* which means our answer is (.707, .707) - the right one
			* OK, but what does it _mean_?
				* You can visualize this as a if the two rows were the axes of a rotated coordinates system
				* illo
			* all a matrix does is represents a series of steps done in series
				* To a vector 
				* or to another matrix (more later)
			* For most cases you can ‘visualize’ a matrix by  imagining each row in the matrix is the vector which defines one axis of a coordinate system
				* This has a neat side effect: if those vectors are at right angles to each other (like they were in our 45 degree rotation example)  then the matrix will rotate the vector but not change it’s magnitude
					* this is an ‘orthonormal’ matrix
				* If the basis vectors of the matrix are not orthogonal then they vector will be scaled as well as rotated. If you do this to a series of points, this produces a skewed figure
				* Example:
					* double the second vector in the t20
			* This simplified example in 2d extends naturally to 3 dimensions  as well. Let’s turn our matrix into 3d by making each row into a 3d vector:
			* (.707,.707,0)
			* (-.707,.707,0)
			* (0,0,1)
			* That last row is the z axis.  Multiplying this out gives
			* (1,0,0) dot (.707,-.707, 0) = .707
			* (1,0,0) dot (.707,.707, 0) = .707
			* (1,0,0) dot (0,0,1) = 0
			* As you can see the result is the same: our original 2d rotation was implicitly around the Z axis.  illo
			* If we wanted to rotate around the X axis instead we’d be changing the Y and Z rows of the matrix. So a matrix like this:  
				1,0,0  
				0 .707, -.707  
				0 .707, .797
			* multiplied by our original vector (1,0,0):  
				(1,0,0) dot (1,0,0) = 1  
				(1,0,0) dot (0, .707, .707) = 0  
				(1,0,0) dot (0,-.707, .707) = 0
			* which is an unchanged vector. Since our original vector lies on the X axis, this is exactly what we’d expect.  If we tried a vector pointing along Z, however:
			* (0,0,1) dot (1,0,0) = 0
			* (0,0,1) dot (0, .707, -.707) = -.707
			* (0,0,1) dot (0, .707. .707) = .707
			* this gives is a vector pointing 45 degrees into Y and Z.
			* QA
			* CALLOUT: 
				* building a rotation matrix
				* RotateX =  
					1,0,0  
					0 cosR -sinR  
					0 sinR cosR
				* RotateY =   
					cosR 0 sinR  
					0  1 0   
					-sinR 0 cosR
				* RotateZ =   
					cosR -sinR 0  
					sinR cosR 0  
					0 0 1
		* Scaling a matrix
			* Once you start to visualize the matrix as coordinate system with described by row vectors, it’s pretty easy to see how the  scales work.  Let’s take that 45 degree Z rotation matrix and scale it up in the Z direction so that it looks like this:  
				1,0,0  
				0 .707, -1.14  
				0 .707, 1.414  
				  
				With our Z vector we get
			* (0,0,1) dot (1,0,0) = 0  
				(0,0,1)  dot (0,.707, .707) = .707  
				(0,0,1) dot (0,.-.1414, 1.414) = 1.414  
				for a final vector(0, .707, .1414)
			* this is the result we’d expect from rotating that point 45 degrees and scaling it up in Z by a factor of 2
				* As expected, the ‘length’ of our vector has changed.
				* A matrix like this will change the shape of a series of points 
		* Let’s return to 2d for a moment to show how a scale-only matrix works.  An unscaled 2d matrix would look like this:  
			(1,0)  
			(0,1)
		* It seems intuitive that you could scale the whole thing up by scaling every component, and that’s exactly how a uniform scale works:  A simple 2-d scaling matrix that scales something by 2 would be:  
			(2x1), (2x0)  
			(2x0), (2x1)
		* Remembering the intuition each row of a matrix is an axis of a coordinate system, it seems clear that a non uniform scale would look something like this:  
			(1,0)  
			(0,2)  
			for a matrix that scales in Y but not X.  The same idea extends naturally to 3D
		* QA
	* Multiplying matrices
		* We’ve already seen how to create rotation matrices and scale matrices, and even how to combine them
		* If you’re used to working with 3d apps, you’re familiar with the idea of concatenating transformations: for example, you night want to scale something up before rotating it — or to rotate it before scaling.
		* This raises the question of how you could apply a matrix to another matrix: for example, if you have a our 45 degree rotation matrix and our 2x3 scale matrix, can you combine them into a single matrix?
		* The convention for multiplying matrices is a little confusing when you first see it, but it’s actually fairly simple,
		* We already know that multiplying a vector times a matrix is a series of dot products with the ‘row’ of the vector against the ‘column’ of the matrix
		* A matrix multiplication basically the same operation in two dimensions. here each ‘row’ of the matrix is the dot of that row with the corresponding column
		* So, in a simple case of our scale and rotate matrices  
			(2, 0)      (-.707, 0)  
			(0, 3)      (0, .707)  
			you would have
		* (2,0) dot ( -.707, 0)    (2,0) dot (0,.707)  
			(0,3) dot (-.707, 0)     (0, 3) dot (0, .707)
		* which means   
			(-1.414, 0)  
			(0, 2.121)
		* The same thing works in 3 dimensions:  
			example
		* Theres one extremely important side effect of the way that matrices are calculated. If you change the order of the multiplication, you change the results! This is unlike conventional multiplication. 
		* Heres why this is true. Compare
			* m times m2 (ex)
		* with
			* m2 tims m (ex)
		* As you can see the results are quite noticeably different. You corresponds to something that all TA’s know:
			* create two transforms, parent one to the other
			* add a locator or marker to the child at a relative location of 1,0,0
			* scale the parent by 3,2,1 and rotate the child 
			* Now try scaling the parent and rotating the child.  As you can see, the results are quite different
		* The forward kinematic hierarchy we are familiar with from DCC tools maps is really just a reflection of the way matrix multiplication works .  Hierarchy in Max or Maya equates to priority in matrix multiplication. And, as we know quite well, hierarchy makes a huge difference to the outcome of a multiplication
	* Adding translation
		* So far we’ve covered some general applications of matrices.
			* we’ve shown how you can use a 2d matrix for rotate and scale a 2d point, using the dot product of the vector and each successive column in the matrix to make a new vector
			* We’ve shown that the same idea generalizes to 3 dimensions with a 3d vector and a 3x3 matrix
			* We’ve also shown how matrices are multiplied together - essentially as a kind of layer cake of vector - column dot products
			* And we’ve shown how this maps neatly on to the way transforms work in DCC tools. Each transform in a skeleton is a matrix; the order of multiplication maps on to the order of the hierarchy
		* One thing we have not discussed so far is _translation_: we’ve rotated and scaled our vectors but we have not translated them.
		* the matrices we have used up to now are square: they have the same number of rows as columns
		* What happens when we extend that matrix? Let’s go back to a simple 2d example again.
		* Here’s our old 45 degree rotation matrix
		* (-.707, 0)  
			(0, .707)
		* as you recall, multiplying a vector against this matrix is really taking the dot product of each column in the matrix with the vector.
		* Since dot products are additive, what happens if we add an extra row to our matrix?
		* (-.707, 0)  
			(0,.707)  
			(1,1)
		* Now if we dot the 

	* Matrix transformations
	## * Translation
(Recap)

We have shown how to use 2x2 and 3x3 matrices to rotate and scale vectors. But any 3d veteran will be wondering how to represent translations.

We've spent a lot of time with dot products. We know that dots are additive - if you dot two vectors, you sum up all of the products. This suggests that maybe we can find a way to tack on more information to our vectors as a way of adding a translation.

Vector—matrix multiplication, you'll recall, is just a series of dot products between the vector and the columns of the matrix.   If we want to stuff extra information into our matrix to hold translation, we want to stick it at the end of the columns so we can add it to our results.  

Let's try to add an offset to a a vanilla 3x3 matrix:
(1,0,0)
(0,1,0)
(0,0,1)
(1,2,3)
Max users will find this familiar— max script makes extensive use of 3x4 matrices for object transforms.

We immediately run into a problem if we try to multiply our vector against this matrix, however. The columns now have 4 items but our vector only has 3. How can we sum up ?

- illo

Obviously, we are going to need to extend our vector to grab the translation values from the new matrix row. As an experiment, let's tack on a zero. This seems like a natural idea, since we know that the 2d vector x,y is equivalent to the 3d vector x,y,0. Let"s see what happens if we do the dot products

1,0,0,0 dot 1,0,0,3 = 1
1,0,0,0 dot 0,1,0,4 = 0
1,0,0,0 dot 0,0,1,5 = 0

Uh oh. The extra zero has allowed us to do the dot product —— but it's also zeroing out the translation we are trying to add. 

That suggest wed like to change that last component to a 1:

1,0,0,1 dot 1,0,0,3 = 4
1,0,0,1 dot 0,1,0,4 = 4
1,0,0,1 dot 0,0,1,5 = 5

There, at last, is the translation we are looking for. 

This still leaves us with an interesting conundrum. It's easy to intuit the meaning of an xyz vector as a 3d coordinate. But what is that last w—coordinate supposed to mean? 

You may remember when we first started discussing vectors that we pointed out that a vector is a general term, encompassing any bundle of numbers. 3d points can be represented by vectors — but so could any bundle of 3 numbers which formed part of a linear equation — say, the value of the dollar, the euro and the yen on a given day. Dot products and matrices work the same way regardless of the subject matter.

In 3d graphics, often talk about vectors when we really mean Euclidean vectors: a set of xyz numbers which represent a spatial offset. That offset is a purely relative quantity — it represents a change in position, but not a position. An obvious example is a surface normal— the normal of a 3d plane might be (0,1,0) and won't change even of the plane is moved.

At the same time we often deal with 3d points which are not offsets, but actual positions. Our plane might keep its normal as it moves but it's translation value will change.

The difference between “pure” vectors and points is an important one. It also maps quite nicely onto that 4th coordinate we added to our vector. An xyzw vector ending in a zero is a pure offset vector —  it represents abstract spatial delta, rather than the a distance between two particular points in space.  An xyzw vector ending in 1, on the other hand, is a geometric point which can be translated.  That last component in the vector preserves the contribution of the last row in the matrix


So now we have a pretty complete convention for representing both points and vectors and also for transforming them with translations rotations and scales.

There is one flaw in the system, however. Our 4-part vectors let us distinguish between points and pure vectors, but out 3\*4 matrix is giving us back 3 components not 4 — it is losing information we might need to keep (for example, if we wanted to multiply a point by several matrices in series) . If we want to get a 4—way vector back from the matrix we are going to need an extra column.

Luckily, we know what we want from that extra column — we just need to preserve that w value and nothing else. Since only the last item in the column should have any value, we can fill the first 3 places with zeroes. The final item is a one — that way, when we dot this column against the our original xyzw vector it will return a 1 for points and a zero for vectors.

Illo

It has been a long road, but we have finally arrived at the 4x4 matrix, the last of the building blocks of 3d math.  Every 3d application uses 4x4 matrices to build and animate and display 3d objects.   multiplying a vector by a matrix is an efficient and elegant way to express the idea we usually describe as parenting: vector (1,0,0,1) times matrix *example* means “where is point 1,0,0 of a coordinate system rotated by X and located at Y.  

Multiplying two matrices (sometimes also called ‘concatenating’ those matrices) transforms the first matrix into the space of the second. As we pointed out above, the order of the multiplication matters a great deal: a times b does not equal b times a in matrix math!  This is a common source of confusion and pain for 3d programmers of all levels.

perspective matrices
* TBD

“Coookbook”
* dot product
	* dp as projection of a vector onto another
	* extrude a vert along a normal
		* if you have discontinuous normals, like a corner, adding them up and averaging will not give you the right depth
		* Illo
		* take the dot of the average normal each vertex normal in turn
		* This gives you how closely the averaged normal matches the originals
			* on a plane, the dot will be one and so nothing needs to be done
			* On an acute angle the dot can be pretty small
			* so you can figure out how much to scale the averaged normal using 1/the projection values
			* Ex one a right angle, the dot between the average normal and each vertex normal will be .707
			* 1/.707 = 1.414 = srqt of 2  =the right extrusion
	* Dot as projection in animation
		* Dot the vector from COG to ground against vector gravity
			* gives a scaled idea of how ‘off center’ a character is
	* Dot in rendering
		* the dot of two normalized vectors is the cosine of the angle between them
		* This  is the core of the rendering equation: Normal dot Lighting = diffuse illumination
		* Knowing this you can ‘cheat’ in some interesting ways:
			* Remap the result of the dot for sharper or softer terminators
		* De-normalizing either the light or the normal vectors can be a proxy for something other than conventional lighting
			* shorten or lengthen the surface normal to control the surface reflectivity
			* Shorten or lengthen the light vector to reflect light intensity
			* 
		* Fresnel
			* Dot a surface normal against the view dir
			* example
	* dot as selection
		* You can use a dot as a mathematical shorthand for a number of logical and checks.  
		* Eg: v1 = (1,2,3,4,5)
		* v2 = (0,0,0,1,0)
		* v1 dot v2 = 4
		* This is handy for applications like shaders where you may have essentially ‘pick from a list’ without conventional programming flow control
		* This can also be a good weight of doing weighted sums:
		* prices = (10, 20, 25, 50)
		* orders = (0, 3, 1, 2)
		* prices dot orders = 185
		* 

