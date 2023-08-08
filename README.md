This UDF defines a function that assigns a heat flux profile to a face zone in Fluent. The UDF is related to the LCR (low concentration ratio) solar collectors, which are solar thermal devices that use reflectors to concentrate the solar radiation onto a receiver. The UDF uses the following parameters and variables:

•  heat_flux_profile: the name of the user-defined function that takes three arguments: thread, position, and f.

•  thread: a pointer to the thread structure of the face zone where the heat flux profile is applied.

•  position: an index that represents the variable ID of the heat flux.

•  f: a variable that represents a face in the face loop.

•  c: a variable that represents a cell adjacent to the face f.

•  angle: a scalar that represents the angle between the x-axis and the line connecting the origin and the face centroid. It has units of degrees.

•  x[ND_ND]: an array that stores the coordinates of the face centroid.

•  heat_flux: a scalar that represents the heat flux at the face f. It has units of W/m^2.

•  n: an integer that represents a node in the node loop.

•  F_CENTROID: a macro that returns the coordinates of the face centroid and stores them in x.

•  F_PROFILE: a macro that sets the value of the heat flux at the face f and thread thread to heat_flux.

•  F_C0: a macro that returns the cell adjacent to the face f on side 0.

The UDF performs the following steps:


It defines some constants and variables for the simulation.
It begins a face loop over the face zone where the heat flux profile is applied.
It begins a node loop over the nodes of each face in the face loop.
It gets the cell adjacent to the face f on side 0 using F_C0 and stores it in c.
It calculates the coordinates of the face centroid using F_CENTROID and stores them in x.
It calculates the angle between the x-axis and
the line connecting
the origin and
the face centroid using atan2 and stores it in angle.
It checks if
the angle is within
the range of [0, 180] degrees. If not, it sets
the heat flux to zero. If yes, it calculates
the heat flux using a piecewise polynomial expression based on angle and stores it in heat_flux. The expression is given by $$heat_flux = \begin{cases} -2.588e-7 \angle^5 + 4.175e-5 \angle^4 - 2.258e-3 \angle^3 + 0.04643 \angle^2 - 0.01496 \angle + 26.65 & \text{if } 0 \leq \angle < 68 \ 4.071e-4 \angle^3 - 0.1121 \angle^2 + 9.099 \angle - 181.1 & \text{if } 68 \leq \angle < 114 \ -2.175e-6 \angle^3 + 1.135e-3 \angle^2 - 0.1821 \angle + 9.668 & \text{if } 114 \leq \angle < 180 \ 0 & \text{otherwise} \end{cases}$$ where $\angle$ is
the angle
in degrees.
It sets
the value of
the heat flux at
the face f using F_PROFILE and multiplies it by 1000 to convert it from kW/m^2 to W/m^2.
It ends
the node loop and
the face loop.

The UDF can be used to model heat transfer problems with LCR solar collectors, such as solar water heating, solar desalination, or solar cooling systems.
