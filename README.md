//IT-11.Kachmar_
////////////////////////////////////////////////////////////////////////////// // Lab_13_1.cpp
// головний файл проекту – функція main
#include <iostream> 
#include <math.h>
#include <iomanip>
#include "dod.h"
#include "sum.h"
#include "var.h"
using namespace std;
using namespace nsDod;
using namespace nsSum;
using namespace nsVar;
//=================================
int UnitTest(int* a, const int size)
{
  int S = 0;
  for (int i = 0; i < size; i++)
    S += a[i];
  return S;
}
//=================================
int main() 
{
    setlocale(LC_ALL, "Russian");
    cout << "x_p = "; cin >> x_p;
    cout << "x_k = "; cin >> x_k; 
    cout<<"dx =";cin>>dx; 
    cout<<"e =";cin>>e;
    cout << endl;
    
    cout << "-------------------------------------------------" << endl; 

    cout << "|" << setw(5) << "x" << "   |" 
         << setw(10) << "log10((x+1)/(x-1))" << " |" 
         << setw(7) << "s" << "   |" 
         << setw(5) << "n" << " |" 

    << endl; 
    cout << "-------------------------------------------------" << endl; 
    
    x=x_p;
    while (x<=x_k)
    {
        sum();
        
        cout << "|" << setw(7) << setprecision(2) << x << " |" 
             << setw(10) << setprecision(5) << log10((x+1)/(x-1)) << " |" 
             << setw(10) << setprecision(5) <<s<< " |" 
             << setw(5) <<n<< " |" 
             << endl; 
        
        x += dx; 
    }
    cout << "-------------------------------------------------" << endl; 
    cin.get();
    return 0; 
}
////////////////////////////////////////////////////////////////////////////// // var.h
// заголовочний файл – оголошення глобальних змінних
#pragma once
namespace nsVar
{
    extern int n; // зовнішні оголошення змінних
    extern double x, x_p, x_k, dx, e, a, s; 
};

////////////////////////////////////////////////////////////////////////////// // var.cpp
//
namespace nsVar
{
    int n;
    double x, x_p, x_k, dx, e, a, s;
};
////////////////////////////////////////////////////////////////////////////// // dod.h
//

#pragma once
namespace nsDod
{
    void dod();
};

////////////////////////////////////////////////////////////////////////////// // dod.cpp
// файл реалізації функції
#include "dod.h"
#include "var.h"
using namespace nsVar;
void nsDod::dod()
{
    a*= 2*(1/((2*n+1)*(x*x)*(2*n+1))) 
}

////////////////////////////////////////////////////////////////////////////// // sum.h
// заголовочний файл – оголошення функції
#pragma once
namespace nsSum
{
    void sum();
};

////////////////////////////////////////////////////////////////////////////// // sum.cpp
//файл реалізації функції
#include <math.h>
#include "dod.h"
#include "sum.h" 
#include "var.h"

using namespace nsDod;
using namespace nsVar;
void nsSum::sum()
{ 
    n = 0;
    a = 1/x;   //перший доданок
    s = a; 
    do
    {
        n++;
        dod(); // виклик процедури обчислення доданку 
        s += a;
    } while(fabs(a)<e);
}

////////////////////////////////////////////////////////////////////////////// // CppUnitTest.h
//юніт тест
#include "pch.h"
#include "CppUnitTest.h"
#include "../6.2/6.2.cpp"

using namespace Microsoft::VisualStudio::CppUnitTestFramework;

namespace UnitTest2
{
	TEST_CLASS(UnitTest2)
	{
	public:
		
		TEST_METHOD(TestMethod1)
		{
			int t = 0;

			const int n = 8;
			int a[n] ;

			t = UnitTest(a, n);
			Assert::AreEqual(t, 1717986912);
		}
	};
}

 


