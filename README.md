# package CCE;

import java.util.Scanner;
import java.util.*;

class item{
	String code;
	String name;
	int quantity;
	
	
	item(String code, String name, int quantity){
		this.code = code;
		this.name = name;
		this.quantity = quantity;
			
	}
	
	public String toString() {
		return code + "|" + name  + "|" + quantity ;
	}

	
class Truck{
	String plate;
	String driver;		
	
	
	Truck(String plate, String driver){
		this.plate = plate;
		this.driver = driver;
	}
	public String toString() {
		return plate + "|" + driver;
	}

class WarehouseLoadingSystem{
	ArrayDeque<item> warehouseStack = new ArrayDeque<>();
	ArrayDeque<Truck> truckQueue = new ArrayDeque<>();
	Scanner sc = new Scanner(System.in);
		
	 int choice = -1;

	    while (choice != 0) {
	        System.out.println("\n=== Warehouse Loading System  ===");
	        System.out.println("[1] Store item (push");
	        System.out.println("[2] View warehouse stack");
	        System.out.println("[3] Register arriving truck (enqueue)");
	        System.out.println("[4] View waiting trucks");
	        System.out.println("[5] Load next truck (pop item + poll truck");
	        System.out.println("[0] Exit");
	        System.out.print("Enter choice: ");
	        choice = Integer.parseInt(sc.nextLine());

	        if (choice == 1) {
	            System.out.print("Enter code: ");
	            String Code = sc.nextLine();
	            System.out.print("Enter name: ");
	            String Name = sc.nextLine();
	            System.out.print("Enter quantity: ");
	            int Quant = sc.nextInt();

	            item i = new item(Code, Name, Quant);
	            warehouseStack.push(i);
	            System.out.println("Stored: " + i);

	        } else if (choice == 2) {
	            if (warehouseStack.isEmpty()) {
	                System.out.println("No items present at the warehouse.");
	            } else {
	                System.out.println("TOP →");
	                for (item i : warehouseStack) {
	                    System.out.println(i);
	                }
	                System.out.println("← BOTTOM");
	            }

	        } else if (choice == 3) {
	            System.out.print("Enter truck plate: ");
	            String plate = sc.nextLine();
	            System.out.print("Enter driver name: ");
	            String driver = sc.nextLine();

	            Truck truck = new Truck(plate, driver);
	            truckQueue.offer(truck);
	            System.out.println("Registered: " + truck);

	        } else if (choice == 4) {
	            if (truckQueue.isEmpty()) {
	                System.out.println("No trucks waiting.");
	            } else {
	                System.out.println("FRONT →");
	                for (Truck truck : truckQueue) {
	                    System.out.println(truck);
	                }
	                System.out.println("← REAR");
	            }

	        } else if (choice == 5) {
	            if (warehouseStack.isEmpty() || truckQueue.isEmpty()) {
	                System.out.println("Cannot load. Either no items or no trucks.");
	            } else {
	                item i = warehouseStack.pop();
	                Truck truck = truckQueue.poll();
	                System.out.println("Loaded: " + i + " → " + truck);
	                System.out.println("Remaining items: " + warehouseStack.size());
	                System.out.println("Remaining trucks waiting: " + truckQueue.size());
	            }

	        } else if (choice == 0) {
	            System.out.println("Exiting program...");
	        } else {
	            System.out.println("Invalid choice. Try again.");
	        }
	    }
