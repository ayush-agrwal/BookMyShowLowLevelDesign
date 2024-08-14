# BookMyShowLowLevelDesign
## this repo contains the code that follow the design in the attached image 

#### Multiple users might try to book the same seat at the same time, so it's crucial to handle concurrency correctly to avoid overbooking.

#### Pessimistic Locking
Pessimistic locking assumes that conflicts will happen and locks the seat as soon as a user starts the booking process. This ensures that no other user can book the same seat while the first user is completing their booking.

##### How It Works:
User A selects a seat and begins the booking process.
The system applies a lock to that seat, preventing other users from booking it until User A completes the transaction.
If User A finishes booking, the seat is marked as booked and the lock is released.
If User A cancels or fails to complete the booking within a certain time, the lock is eventually released so that the seat can be made available again.

##### Benefits:

Prevents any other bookings for the same seat while the current user is booking it.
Ensures data consistency.
##### Drawbacks:

Can lead to delays for other users if the lock is held for too long.
May reduce system throughput due to locking.

#### Optimistic Locking
Optimistic locking assumes that conflicts are rare and doesn’t lock the seat immediately. Instead, it checks for conflicts when the user submits their booking request. If the seat has already been booked by someone else in the meantime, the system handles the conflict.

##### How It Works:
User A selects a seat and begins the booking process.
The system allows User A to proceed without immediately locking the seat.
When User A completes the booking request, the system checks if the seat is still available.
If the seat is still available, the booking is processed and the seat is marked as booked.
If the seat has been taken by another user in the meantime, User A is informed and may need to choose a different seat or retry the booking.


##### Benefits:

Allows more users to attempt bookings simultaneously.
Can improve performance and system throughput

##### Drawbacks:

Requires conflict handling logic and may lead to booking failures.
Might not be suitable for systems where conflicts are frequent.
