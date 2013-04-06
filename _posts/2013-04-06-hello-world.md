---
layout: post
title: Hello, World!
---

This is my first post for testing a couple of Jekyll features.

Code embedding using [pygments](http://pygments.org/): `std::out << "Hello, World!"`. Block of code:

{% highlight c++ %}
#include <iostream>

using namespace std;

int main(int argc, char **argv) {
  cout << "Hello, World!" << endl;
  return 0;
}
{% endhighlight %}

Why don't we tryout some BlahTeX: $Y(\omega) = \log_{10} \left| \sum_{n=0}^{N-1}
y(n) e^{-2\pi\omega n/N} \right|$. BlahTex supports a subset of TeX, including
almost all of the symbols. Full documentation [here](http://gva.noekeon.org/blahtexml/blahtexml-0.9-doc.pdf).
