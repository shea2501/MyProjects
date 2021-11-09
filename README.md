# MyProjects



import java.util.Scanner;

public class CoffeeMachine {

    public static int water = 400;
    public static int milk= 540;
    public static int beans = 120;
    public static int cups= 9;
    public static int money = 550;
    public static int needsWaterEsp = 250;
    public static int needsBeansEsp = 16;
    public static int costEsp = 4;
    public static int needsWaterLat = 350;
    public static int needsMilkLat = 75;
    public static int needsBeansLat = 20;
    public static int costLat = 7;
    public static int needsWaterCappu = 200;
    public static int needsMilkCappu = 100;
    public static int needsBeansCappu = 12;
    public static int costCappu = 6;
    enum States {
        PENDING, CHOOSE_COFFEE, FILL_WATER, FILL_MILK, FILL_BEANS, FILL_CUPS

    }
    static States actualState = States.PENDING;

    public static void displayState() {

        switch (actualState) {
            case PENDING:
                System.out.println("Write action (buy, fill, take, remaining, exit):");
                break;
            case CHOOSE_COFFEE:
                System.out.println("What do you want to buy? 1 - espresso, 2 - latte, 3 - cappuccino, back - to main menu:");
                break;
            case FILL_WATER:
                System.out.println("Write how many ml of water you want to add:");
                break;
            case FILL_MILK:
                System.out.println("Write how many ml of milk you want to add:");
                break;
            case FILL_BEANS:
                System.out.println("Write how many grams of coffee beans you want to add:");
                break;
            case FILL_CUPS:
                System.out.println("Write how many disposable cups of coffee you want to add:");
                break;
            default:
                break;
        }
    }

    public static void actionSelect(String choice) {

        switch (actualState) {
            case PENDING:
                switch (choice) {
                    case "buy":
                        actualState = States.CHOOSE_COFFEE;
                        break;
                    case "fill":
                        actualState = States.FILL_WATER;
                        break;
                    case "take":
                        System.out.println("I gave you " + money +"$\n");
                        money = 0;
                        actualState = States.PENDING;
                        break;
                    case "remaining":
                        System.out.println("\nThe coffee machine has:");
                        System.out.println(water + " ml of water\n" + milk + " ml of milk");
                        System.out.println(beans + " g of coffee beans\n" + cups + " disposable cups\n$" + money + " of money\n");
                        actualState = States.PENDING;
                        break;
                    case "exit":
                        break;
                    default:
                        break;
                } break;
            case CHOOSE_COFFEE:
                switch (choice) {
                    case "1":
                        if (water >= needsWaterEsp && beans >= needsBeansEsp) {
                            System.out.println("I have enough resources, making you a coffee!\n");
                            water -= needsWaterEsp;
                            beans -= needsBeansEsp;
                            money += costEsp;
                            cups--;
                        } else if (water < needsWaterEsp) {
                            System.out.println("Sorry, not enough water!\n");
                        } else if (beans < needsBeansEsp) {
                            System.out.println("Sorry, not enough beans!\n");
                        }
                        break;
                    case "2":
                        if (water >= needsWaterLat && beans >= needsBeansLat && milk >= needsMilkLat) {
                            System.out.println("I have enough resources, making you a coffee!\n");
                            water -= needsWaterLat;
                            beans -= needsBeansLat;
                            milk -= needsMilkLat;
                            money += costLat;
                            cups--;
                        } else if (water < needsWaterLat) {
                            System.out.println("Sorry, not enough water!\n");
                        } else if (beans < needsBeansLat) {
                            System.out.println("Sorry, not enough beans!\n");
                        } else if (milk < needsMilkLat) {
                            System.out.println("Sorry, not enough milk!\n");
                        }
                        break;
                    case "3":
                        if (water >= needsWaterCappu && beans >= needsBeansCappu && milk >= needsMilkCappu) {
                            System.out.println("I have enough resources, making you a coffee!\n");
                            water -= needsWaterCappu;
                            beans -= needsBeansCappu;
                            milk -= needsMilkCappu;
                            money += costCappu;
                            cups--;
                        } else if (water < needsWaterCappu) {
                            System.out.println("Sorry, not enough water!\n");
                        } else if (beans < needsBeansCappu) {
                            System.out.println("Sorry, not enough beans!\n");
                        } else if (milk < needsMilkCappu) {
                            System.out.println("Sorry, not enough milk!\n");
                        }
                        break;
                    default:
                        break;
                } actualState = States.PENDING; break;


            case FILL_WATER:
                water += Integer.parseInt(choice);
                actualState = States.FILL_MILK;
                break;
            case FILL_MILK:
                milk += Integer.parseInt(choice);
                actualState = States.FILL_BEANS;
                break;
            case FILL_BEANS:
                beans += Integer.parseInt(choice);
                actualState = States.FILL_CUPS;
                break;
            case FILL_CUPS:
                cups += Integer.parseInt(choice);
                actualState = States.PENDING;
                break;
            default:
                break;
        }

    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true) {
            CoffeeMachine.displayState();
            String choice = sc.next();
            if (choice.equals("exit")) {
                System.out.println("exit");
                break;
            } else {
                CoffeeMachine.actionSelect(choice);

            }

        }
    }

}

