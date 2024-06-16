# coffee-machine
This is my recent project done using python
MENU = {
    "espresso": {
        "ingredients": {
            "water": 50,
            "coffee": 18,
        },
        "cost": 1.5,
    },
    "latte": {
        "ingredients": {
            "water": 200,
            "milk": 150,
            "coffee": 24,
        },
        "cost": 2.5,
    }
    "cold coffee": {
        "ingredients": {
            "water": 250,
            "milk": 100,
            "coffee": 24,
        },
        "cost": 3.0,
    }
}
profit = 0
resources = {
    "water": 300,
    "milk": 200,
    "coffee": 100,
}


# def report_before_purchasing():
#     entry=input("What would you like? (espresso/latte/cappucino)").lower()
#     if entry=="report":
#         print(f"{resources}")

def is_resource_sufficient(order_resources, resources):
    for items in order_resources:
        if order_resources[items]>resources[items]:
            print("sorry we are out of resources")
            return False
        return True

def process_coin():
    print("Please insert coins.")
    total=int(input("how many quarters?:"))*0.25
    total+=int(input("how many dimes?:"))* 0.10
    total+=int(input("how many nickles?:"))* 0.05
    total+=int(input("how many penny?:"))*0.01
    return total

def calculate_money(amount_received, direct_cost):

    if amount_received >= direct_cost:
        change = round(amount_received - direct_cost, 2)
        print(f"Here is {change} in change")
        global profit
        profit += direct_cost
        return True
    else:
        print("sorry thats not enough money, money refunded")
        return False

def make_coffee(drink_name, order_ingredient):
    for item in order_ingredient:
        resources[item]-=order_ingredient[item]
        print(f"here is your {drink_name}, Enjoy!")

is_on = True

while is_on:
    drink_name = input("What would you like? (espresso/latte/cappucino)").lower()
    if drink_name == "off":
        is_on = False
    elif drink_name == "report":
        print(f"Water: {resources['water']}ml")
        print(f"Milk: {resources['milk']}ml")
        print(f"Coffee: {resources['coffee']}g")
        print(f"Money: ${profit}")
    else:
        drink = MENU[drink_name]
        if is_resource_sufficient(drink["ingredients"], resources):
            payment = process_coin()
            if calculate_money(payment, drink["cost"]):
                make_coffee(drink_name, drink["ingredients"])

