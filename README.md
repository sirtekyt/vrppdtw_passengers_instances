# vrppdtw_passengers_instances
Instances for testing VRPPDTW.

# code to read
    public static void readInstances(){
        int busCount;
        try {
            File file = new File("dirname");
            Scanner scanner = new Scanner(file);
            String lineOfText = null;
            while(scanner.hasNext()) {
                lineOfText = scanner.nextLine();
                if (lineOfText.startsWith("//")){
                    continue;
                }else {
                    break;
                }
            }
            busCount = Integer.parseInt(lineOfText);
            scanner.nextLine();

            for (int i = 1; i <= busCount; i++) {
                Bus bus = new Bus(depot, 50, true, new ArrayList<>());
                buses.put(i, bus);
            }
            addStopsToListOfStops();
            distanceStops =new DistanceStops(stops.size());

            int number=1;
            while (scanner.hasNextLine()) {
                String line = scanner.nextLine();
                String[] parts = line.split(";");
                int idPickup = Integer.parseInt(parts[0]);
                int idDelivery = Integer.parseInt(parts[1]);
                String[] startTime = parts[2].split(",");
                String[] stopTime = parts[3].split(",");
                Order order = new Order(idPickup, idDelivery, false,
                        LocalDateTime.of(LocalDate.now(), LocalTime.of(Integer.parseInt(startTime[0]), Integer.parseInt(startTime[1]))),
                        LocalDateTime.of(LocalDate.now(), LocalTime.of(Integer.parseInt(stopTime[0]), Integer.parseInt(stopTime[1]))));
                orders.put(number,order);
                number++;
            }
            scanner.close();
            orderHandling();
        } catch (FileNotFoundException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }


    }
