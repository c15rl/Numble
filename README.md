# Numble
CS3 assignment (Dalton)
import java.util.List;
import java.util.Scanner;
import java.util.Arrays;
import java.util.ArrayList;

public class Numble {
	/**
	 * Input
	 * 1. 9768014, 6874514, 9655532
	 * 2. 7, 7, 5, 7, 6
	 * 3. 6, 5, 3, 6, 9
	 * 4. 5, 6, 4, 6, 9
	 * 5. 4, 5, 4, 8, 6
	 * 6. 6, 6, 4, 4, 6
	 * 
	 */

	public static int n_end;

	public static void main(String[] args) {

		// make 2D char array that is 13 by 7
		char[][] board = new char [13][7];
		int counter = 0;

		// put x in all char array positions
		clearBoard(board);

		//organize numbers
		Scanner scan = new Scanner(System.in);
		String[] s = scan.nextLine().split(", ");
		char[] tmp0 = s[0].toCharArray();
		char[] tmp1 = s[1].toCharArray();
		char[] tmp2 = s[2].toCharArray();

		// sort number array
		Arrays.sort(tmp0);
		reverse(tmp0);

		Arrays.sort(tmp1);
		reverse(tmp1);

		Arrays.sort(tmp2);
		reverse(tmp2);

		//get locations
		while(counter<6){
			s = scan.nextLine().split(", ");
			int size0 = Integer.parseInt(s[0]);
			int size1 = Integer.parseInt(s[1]);
			int size2 = Integer.parseInt(s[2]);
			char intersect0 = s[3].charAt(0);
			char intersect1 = s[4].charAt(0);

			// only use number of digits specified
			char[] num0 = new char[size0];
			char[] num1 = new char[size1];
			char[] num2 = new char[size2];

			//num0
			for(int i = 0; i<size0; i++){
				num0[i] = tmp0[i];
			}
			//num1
			for(int i = 0; i<size1; i++){
				num1[i] = tmp1[i];
			}
			//num2
			for(int i = 0; i<size2; i++){
				num2[i] = tmp2[i];
			}


			// write full first number in row 7 of 2D char array
			for(int i = 0; i<size0; i++){
				board[6][i] = num0[i];
			}

			// search horizontal number to find intersecting digit column
			//1st intersection
			int col0 = 0;
			for(int i = 0; i<num0.length; i++){
				if(num0[i] == intersect0){
					col0 = i;
				}
			}
			//System.out.println(col0);

			//2nd intersection
			int col1 = 0;
			for(int i = 0; i<num0.length; i++){
				if(num0[i] == intersect1){
					col1 = i;
				}
			}

			//System.out.println(col1);

			/* write second number vertically starting in row 0, column 0
		for(int i = 0; i<size1; i++){
			board[i][col0] = num1[i];
		}*/


			int ind0 = 0; //#s before point of intersection 
			for(int i = 0; i<num1.length; i++){if(num1[i] == intersect0){ind0 = i;}}
			int ind1 = 0; //#s before point of intersection 
			for(int i = 0; i<num2.length; i++){if(num2[i] == intersect1){ind1 = i;}}

			int offset0 = 6 - ind0;
			for (int i = offset0; i < offset0 + num1.length; i++) {
				board[i][col0] = num1[i-offset0];}

			int offset1 = 6 - ind1;
			for (int i = offset1; i < offset1 + num2.length; i++) {
				board[i][col1] = num2[i-offset1];}
			print(board);
			clearBoard(board);
			counter++;
		}
		// write vertical number in row 0, column from line above


		// search vertical number to find intersecting digit row
		// do little bit of math to find out what row to start printing vertical number on
		// write vertical number in row from line above, and column found before
		// loop to do all five answers
		//
		// upload what you have before permutations
		//
		// permutations of numbers.

	}


	private static void print(char[][] board){
		//System.out.println("board");
		for(int i = 0; i<board.length; i++){
			for(int j = 0; j<board[i].length; j++){
				System.out.print(board[i][j]);
			}
			System.out.println();
		}
	}

	private static void reverse(char[] tmp) {
		for(int i=0; i<3; i++){
			char temp = tmp[i];
			n_end = tmp.length-(1+i);
			tmp[i] = tmp[n_end];
			tmp[n_end] = temp;
			n_end--;
		}
	}
	
	public static void clearBoard(char[][] board){
		for(int i = 0; i<board.length; i++){
			for(int j = 0; j<board[i].length; j++){
				board[i][j] = ' ';
			}

		}
	}


	/*	

	public static int n_end;

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		//the board is the right size
		char[][] board = new char [13][7];
		for(int i = 0; i<board.length; i++){
			for(int j = 0; j<board.length; j++){
				//System.out.print(i + "," + j + "; ");
			}
			//System.out.println();
		}

		Scanner scan = new Scanner(System.in);
		String[] s = scan.nextLine().split(", ");
		int[] numbers = new int[s.length];
		for(int i = 0; i<s.length; i++){
			numbers[i]= Integer.parseInt(s[i]);
			System.out.println("numbers[" + i + "]= " + numbers[i]);
		}

		char[] temp = new char[7];

		//attempt to make each 7 digit number its own array and to separate out all of the digits in the number.
		int[] num0 = getDigits(numbers[0]);
		int[] num1 = getDigits(numbers[1]);
		int[] num2 = getDigits(numbers[2]);

		Arrays.sort(num0);
		reverse(num0);

		Arrays.sort(num1);
		reverse(num1);

		Arrays.sort(num2);
		reverse(num2);

		int pointer = 3;
		for(pointer = 0; pointer<3; pointer++){
			if(pointer==0){
				for(int i = 0; i<num0.length; i++){
					//System.out.println("num0[" + i + "]: " + num0[i]);
				}
			}
			else if(pointer==1){
				for(int i = 0; i<num1.length; i++){
					//System.out.println("num1[" + i + "]: " + num1[i]);
				}	
			}
			else{
				for(int i = 0; i<num2.length; i++){
					//System.out.println("num2[" + i + "]: " + num2[i]);
				}
			}
		}


		//loop this for each set of values
		Scanner loc = new Scanner(System.in);
		s = scan.nextLine().split(", ");
		int[] length = new int[3];
		int[] intersect = new int[2];
		for(int i = 0; i<s.length; i++){
			if (i<3){
				length[i] = Integer.parseInt(s[i]);
				System.out.println("length[" + i + "]= " + length[i]);
			}
			else{
				int n = i-3;
				intersect[n] = Integer.parseInt(s[i]);
				System.out.println("intersect[" + n + "]= " + intersect[n]);
			}


			//number_cutter(length[0], length[1], intersect[0], num0, num1);
			//number_cutter(length[0], length[2], intersect[2], num0, num2);

		}
		cut0(num0, length[0], intersect);

		/* Plan:
	 * 
	 * 1. arrays.aslist
	 * 2. arrays.sort(T[] a, Comparator<? Super T> c)
	 * 3. math.max
	 * 4. Binary search algorithm-> use the input to get the # of digits in the number (int d) then sort the values in the number into an 
	 * array (int[] n). Starting with the greatest number (n[0]), add the first d numbers to get value (v) and if v%5 != 0 swap the last 2 
	 * numbers. If all the values with the greatest number don't fit, move on to the next largest value and so on.
	 * http://video.franklin.edu/Franklin/Math/170/common/mod01/binarySearchAlg.html 
	 * 5. Princeton permutation: http://aofa.cs.princeton.edu/lectures/lectures13/AA07-Perms.pdf
	 */
	/*
}

	private static void reverse(int[] num) {
		for(int i=0; i<3; i++){
			int temp = num[i];
			n_end = num.length-(1+i);
			num[i] = num[n_end];
			num[n_end] = temp;
			n_end--;
		}
	}



	//I took this from: http://stackoverflow.com/questions/3389264/how-to-get-the-separate-digits-of-an-int-number
	public static int[] getDigits(int num) {
		List<Integer> digits = new ArrayList<Integer>();
		collectDigits(num, digits);
		int[] intarray = new int[digits.size()];
		for(int i = 0; i<digits.size(); i++){
			intarray[i] = digits.get(i);
		}

		return intarray;
		//return digits.toArray(new Integer[]{});
	}

	//I took this from: http://stackoverflow.com/questions/3389264/how-to-get-the-separate-digits-of-an-int-number
	private static void collectDigits(int num, List<Integer> digits) {
		if(num / 10 > 0) {
			collectDigits(num / 10, digits);
		}
		digits.add(num % 10);
	}

	public static void cut0(int[] num0, int length0, int[] intersect){
		System.out.println("in cut0");
		int[] temp0 = new int[length0+1];
		System.out.println("new int[" + length0 + "]");
		int i1 = 0;
		int i2 = 0;
		//System.out.println("length0: " + length0);
		//filling a temporary array with the numbers that should be in num0[]
		if(length0<7){
			for(int j = 0; j<intersect.length; j++){
				System.out.println(" inside intersect[" + j + "]");
				for(int i = 0; i<num0.length; i++){
					if(intersect[j]==num0[i]){
						System.out.println("intersect=num"+"\n intersect[" + j + "] = " + intersect[j] + "\n num0[" + i + "]= " + num0[i]);
						if(j==0){
							i1 = intersect[j]; 
							System.out.println("i1= " + i1);
						}
						else{
							i2 = intersect[j];
							System.out.println("i2= " + i2);
						}

						Math.max(i1, i2);

						if(length0<=i+1){
							System.out.println("intersect=num[" + i + "] and length0<=i+1");
							if(i1>i2){
								temp0[length0]=i1;
								temp0[length0-1]=i2;
								temp0[7]=(Integer) null;
							}
							else{
								System.out.println("intersect=num[" + i + "] and length0>i+1");
								temp0[length0]=i2;
								temp0[length0-1]=i1;
							}

						}
						else{
							temp0[i]=num0[i];
						}

					}
					else{
						System.out.println("intersect[" + j + "] = " + intersect[j] + "\n num0[" + i + "]= " + num0[i]);
						temp0[i]= num0[i];
					}
				}
			}
		}

		else{
			System.out.println("length0= " + length0);
		}

		for(int i = 0; i<temp0.length; i++){
			System.out.println("temp0[" +i+ "]: " +temp0[i]);
		}

	}

	public static void number_cutter(int length0, int lengthx, int intersect, int[] num0, int[] numx){
		int[] tempx = new int[lengthx];
		if(lengthx<7){
			for(int i = 0; i<numx.length; i++){
				if(intersect==numx[i] && lengthx<=i){
					tempx[i]=intersect;
				}
				else{
					tempx[i]= numx[i];
				}
			}
		}
	}
	 */

}//class
