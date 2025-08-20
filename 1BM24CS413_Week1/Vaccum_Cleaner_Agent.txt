import random

rooms = {"A": random.choice(["Clean","Dirty"]),
         "B": random.choice(["Clean","Dirty"])}

def simple_reflex(rooms):
    loc = "A"
    for _ in range(4):
        if rooms[loc]=="Dirty":
            print(loc,"is Dirty → Clean")
            rooms[loc]="Clean"
        else:
            loc = "B" if loc=="A" else "A"
            print("Move to",loc)

def goal_based(rooms):
    loc="A"
    while "Dirty" in rooms.values():
        if rooms[loc]=="Dirty":
            print(loc,"is Dirty → Clean")
            rooms[loc]="Clean"
        else:
            loc = "B" if loc=="A" else "A"
            print("Move to",loc)
    print("Goal Achieved: All rooms clean")
    
print("\n--- Simple Reflex Agent ---")
r1={"A":"Dirty","B":"Clean"}
print("Start:",r1)
simple_reflex(r1)

print("\n--- Goal Based Agent ---")
r2={"A":"Dirty","B":"Dirty"}
print("Start:",r2)
goal_based(r2)
