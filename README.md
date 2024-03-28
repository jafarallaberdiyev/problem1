import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        String village = scanner.next();
        
        String result = possibleSolution(N, village);
        System.out.println(result);
        
        scanner.close();
    }
    
    public static String possibleSolution(int N, String village) {
        char[] houses = village.toCharArray();
        int numHouses = 0;
        for (char house : houses) {
            if (house == 'H') {
                numHouses++;
            }
        }
        
        // Calculate the minimum reachable grids for each person
        int minReachableGrids = Integer.MAX_VALUE;
        for (int i = 0; i < N; i++) {
            if (houses[i] == 'H') {
                int left = i, right = i;
                while (left >= 0 && houses[left] == 'H') left--;
                while (right < N && houses[right] == 'H') right++;
                minReachableGrids = Math.min(minReachableGrids, right - left - 1);
            }
        }
        
        // Check if it's possible to divide the houses
        for (int i = 0; i < N; i++) {
            if (houses[i] == 'H') {
                int left = i, right = i;
                while (left >= 0 && houses[left] == 'H') left--;
                while (right < N && houses[right] == 'H') right++;
                if (right - left - 1 > minReachableGrids) {
                    return "NO";
                }
            }
        }
        
        // Construct the fence configuration
        char[] fence = new char[N];
        for (int i = 0; i < N; i++) {
            if (houses[i] == '.') {
                fence[i] = 'B';
            } else {
                fence[i] = houses[i];
            }
        }
        
        return "YES\n" + new String(fence);
    }
}
