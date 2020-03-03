# I, Suraj Singh, student id: 000742243, certify that all code submitted is my own work; that I have not copied it from any other source. I also certify that I have not allowed my work to be copied by anyone.

/**
* Do use camelCasing for method arguments and local variables.
* Do use predefined type names instead of system type names like Int16, Single, UInt64, etc
* Do use implicit type var for local variable declarations. Exception: primitive types (int, string, double, etc) use predefined names.
* Do organize namespaces with a clearly defined structure
* Do vertically align curly brackets.
*/

using System;
using System.Collections.Generic;

namespace COMP10066_Lab4
{
    /**
     * Library of statistical functions using Generics for different statistical
     * calculations.
     * 
     * see http://www.calculator.net/standard-deviation-calculator.html
     * for sample standard deviation calculations
     *
     * @author Joey Programmer
     */


        /// <summary>
        /// Main Class 
        /// </summary>
    public class Assign4
    {
        /// <summary>
        /// Calculates Average of numbers
        /// Double value which is the average of a list of double data inputs
        /// </summary>
        /// <param name="dataInputs">A list of double value numbers</param>
        /// <param name="includeNegative"> Boolean Input
        /// True means negative values are to be included in calculating average
        /// False means negative values are to be excluded in calculating average
        /// </param>
        /// <returns></returns>
        public static double averageCalculate(List<double> dataInputs, bool includeNegative)
        {
            //Calculate the sum of dataInputs
            double sumInputs = sumCalculate(dataInputs, includeNegative);
            int sumCount = 0;

            //Use for Loop to calculate number of inputs
            for (int i = 0; i < dataInputs.Count; i++)
            {
                // Can include negative numbers
                if (includeNegative || dataInputs[i] >= 0)
                {
                    sumCount++;
                }
            }

            // Check for sumCount equals zero
            if (sumCount == 0)
            {
                throw new ArgumentException("no values are > 0");
            }
            return sumInputs / sumCount;
        }


        /// <summary>
        /// Calculates Sum of numbers
        /// Double value which is the sum of a list of double data inputs
        /// </summary>
        /// <param name="dataInputs">A list of double value numbers</param>
        /// <param name="includeNegative"> Boolean Input
        /// True means negative values are to be included in calculating sum
        /// False means negative values are to be excluded in calculating sum
        /// </param>
        /// <returns></returns>
        public static double sumCalculate(List<double> dataInputs, bool includeNegative)
        {
            //Check if data inputs is empty
            //Use Throw Exception incase of empty input
            if (dataInputs.Count < 0)
            {
                throw new ArgumentException("x cannot be empty");
            }

            //Calculate the sum of dataInputs
            double sumInputs = 0.0;

            //Use for foreach Loop to calculate number of dataInputs
            foreach (double val in dataInputs)
            {
                // Can include negative numbers
                if (includeNegative || val >= 0)
                {
                    sumInputs += val;
                }
            }
            return sumInputs;
        }

        /// <summary>
        /// Calculates median of numbers
        /// </summary>
        /// <param name="dataInputs">A list of double value numbers</param>
        /// <returns>Double value which is the sum of a list of double data inputs</returns>
        public static double medianCalculate(List<double> dataInputs)
        {
            //Check if data inputs is empty
            //Use Throw Exception incase of empty input
            if (dataInputs.Count == 0)
            {
                throw new ArgumentException("Size of array must be greater than 0");
            }

            // Use sorting for dataInputs (ascending)
            dataInputs.Sort();

            // Calculate the median using dtaInputs
            double medianCalculate = dataInputs[dataInputs.Count / 2];
            if (dataInputs.Count % 2 == 0)
                medianCalculate = (dataInputs[dataInputs.Count / 2] + dataInputs[dataInputs.Count / 2 - 1]) / 2;

            // Return Median
            return medianCalculate;
        }

        /// <summary>
        /// Calculates Standard Deviation of numbers
        /// </summary>
        /// <param name="dataInputs">A list of double value numbers</param>
        /// <returns>Double value which is the sum of a list of double data inputs</returns>
        public static double standardDeviation(List<double> dataInputs)
        {
            //Check if data inputs has 2 inputs
            //Use Throw Exception incase of less input
            if (dataInputs.Count <= 1)
            {
                throw new ArgumentException("Size of array must be greater than 1");
            }

            int n = dataInputs.Count;
            double s = 0;
            double a = averageCalculate(dataInputs, true);

            for (int i = 0; i < n; i++)
            {
                double v = dataInputs[i];
                s += Math.Pow(v - a, 2);
            }
            double stdev = Math.Sqrt(s / (n - 1));
            return stdev;
        }

        // Simple set of tests that confirm that functions operate correctly
        static void Main(string[] args)
        {
            List<Double> testDataD = new List<Double> { 2.2, 3.3, 66.2, 17.5, 30.2, 31.1 };

            Console.WriteLine("The sum of the array = {0}", sumCalculate(testDataD, true));

            Console.WriteLine("The average of the array = {0}", averageCalculate(testDataD, true));

            Console.WriteLine("The median value of the Double data set = {0}", medianCalculate(testDataD));

            Console.WriteLine("The sample standard deviation of the Double test set = {0}\n", standardDeviation(testDataD));
        }
    }
}
