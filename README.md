# PlaceHolder
- - - - - - - - - - - - - - - - - - - - - - - - - - -
    
```cpp
#include <iostream>

// Map //////////

template <class T>
struct t_val {
    static decltype(T::value) value;
};

template <class T>
decltype(T::value) t_val <T>::value = { };

// Map //////////


// Placeholders /

using $$0 = struct { int value; };
using $$1 = struct { int value; };
using $$2 = struct { int value; };
using $$3 = struct { int value; };
using $$4 = struct { int value; };

// Placeholders /


// Initializer //

template <class T>
struct $$ {
    T operator= (decltype(T::value) value) const & {
        return T{ value };
    }
};

/*
    with the expression ($$ <TYPE>{} = NUMBER), where TYPE is $$0 $$1 $$2 $$3 or $$4 returns TYPE{ NUMBER }
*/

// Initializer //


// request //////

struct request {
    struct getT_val {
        template <class T>
        operator T() { return T{ t_val <T>::value }; }
    };

    // Constructor //

    /*

        args::element.value is assigned to t_val <$$0>::value
        args::element.value is assigned to t_val <$$1>::value
        args::element.value is assigned to t_val <$$2>::value
        args::element.value is assigned to t_val <$$3>::value
        args::element.value is assigned to t_val <$$4>::value

    */

    template <class... types>
    request(types... args) : request(([&]() { ((t_val <types>::value = args.value), ...); }(), 0))
    {
    }

    // Constructor //


    // Assignment //

    $$0 _0 = getT_val{}; $$1 _1 = getT_val{};
    $$2 _2 = getT_val{}; $$3 _3 = getT_val{};
    $$4 _4 = getT_val{};

    //getT_val's conversion operator deduces the type in the left hand of the assignment
    //and then returns the value contained in the Map for the type

    // Assignment //

    private: request(int) {}
};

// request //////

namespace xt {
    $$ <$$0> $0;
    $$ <$$1> $1;
    $$ <$$2> $2;
    $$ <$$3> $3;
    $$ <$$4> $4;
}

int main() {
    using namespace xt;

    request F {
        $4 = 14, // (1) returns '$$4{ 14 }' (2) assign 14 to 't_val <$$4>::value' (3) assign '$${ 14 }' to '_4'
        $0 = 10, // (1) returns '$$0{ 10 }' (2) assign 10 to 't_val <$$0>::value' (3) assign '$${ 10 }' to '_0'
        $2 = 12, // (1) returns '$$2{ 12 }' (2) assign 12 to 't_val <$$2>::value' (3) assign '$${ 12 }' to '_2'
        $1 = 11, // (1) returns '$$1{ 11 }' (2) assign 11 to 't_val <$$1>::value' (3) assign '$${ 11 }' to '_1'
        $3 = 13  // (1) returns '$$3{ 13 }' (2) assign 13 to 't_val <$$3>::value' (3) assign '$${ 13 }' to '_3'
    };																   

    std::cout << F._0.value << ' ';
    std::cout << F._1.value << ' ';
    std::cout << F._2.value << ' ';
    std::cout << F._3.value << ' ';
    std::cout << F._4.value << ' ';
    return 0;
}
```

1: Veritas - https://godbolt.org/z/Bz2T-1 \
2: Melak47 - https://godbolt.org/z/KCTB3X \
3: Cxx     - README.md
