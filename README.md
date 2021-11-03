# muunits
Units which take advantage of C# 10 abstract interface members

# Base types

namespace Mu.Units

interface IAddable<T>
  where T : IAddable<T>
  {
    static abstract operator+(IAddable<T> left, IAddable<T> right);
  }
  
interface ISubtractable<T>
   where T : ISubtractable<T>
  {
  static abstract operator-(IAddable<T> left, IAddable<T> right);
  }
  
  interface IMultiplicatable<T>
  where T: 
  {
  static abstract operator*(IAddable<T> left, IAddable<T> right);
  }
  
interface IDivisible<T>

interface IScalar<T> : IAddable<T>, ISubtractable<T>, IMultiplicatable<T>, IDivisible<T>
  where T: IScalar<T>
  {
  static abstract IScalar<T> Zero;
  static abstract From(T value);
  static abstract To(T value);
  }
  
  // Classes and structs (including built-ins) can implement interface
struct Int32 : …, IScalar<Int32>
{
    static Int32 I.operator +(Int32 x, Int32 y) => x + y; // Explicit
    static Int32 I.operator -(Int32 x, Int32 y) => x - y; // Explicit
    public static int Zero => 0;                          // Implicit
}

struct Double: _, IScalar<Double>
{
    static Double I.operator +(Int32 x, Int32 y) => x + y; // Explicit
    public static int Zero => 0;                          // Implicit
}
  
struct Distance<T> : IScalar<T>
struct Duration<T> : IScalar<T>
struct Force<T> : IScalar<T>
  
interface ICompoundScalar<T, TOver, TUnder>
    where TOver : IScalar<T>
    where TUnder : IScalar<T>
  {
  }
  
 class Unit<IScalar<T>>
  



