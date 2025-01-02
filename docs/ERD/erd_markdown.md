// Use DBML to define your database structure
// Docs: https://dbml.dbdiagram.io/docs

Table concert {
  id integer [primary key]
  title varchar
  artist varchr
  place varchr
  created_at timestamp 
}

Table concert_schedule {
  id integer [primary key]
  concert_id integer
  concert_date timestamp 
  reservation_start_at timestamp
  created_at timestamp
}

Table concert_seat {
  id integer [primary key]
  concert_schedule_id integer
  seat_level enum
  status enum
  created_at timestamp
  updated_at timestamp
}

Table waiting {
  id integer [primary key]
  user_id integer
  concert_id integer
  created_at timestamp
  updated_at timestamp
  sequence integer
  status enum
}

Table user {
  id integer [primary key]
  user_name varchar
  age integer
  point integer
  created_at timestamp
}

Table point_history {
  id integer [primary key]
  user_id varchar
  amount integer
  type enum
  created_at timestamp
  status varchr
}

Table reservation {
  id integer [primary key]
  user_id integer
  concert_schedule_id integer
  seat_id integer
  status enum
  created_at timestamp
}

Ref: concert_schedule.concert_id > concert.id // many-to-one
Ref: concert_seat.concert_schedule_id > concert_schedule.id
Ref: reservation.concert_schedule_id - concert_schedule.id
Ref: reservation.concert_schedule_id - concert_seat.id
Ref: user.id < point_history.user_id
Ref: user.id < reservation.user_id
Ref: user.id - waiting.user_id