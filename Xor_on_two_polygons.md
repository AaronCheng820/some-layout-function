from operator import xor
points1 = [pya.Point(0/0.001,-10/0.001), pya.Point(0/0.001,0/0.001), pya.Point(4/0.001,0/0.001), pya.Point(4/0.001, -10/0.001)]
points2 = [pya.Point(-3/0.001,-7/0.001), pya.Point(-3/0.001,0/0.001), pya.Point(5/0.001,0/0.001), pya.Point(5/0.001,-7/0.001)]

a = pya.Region(pya.Polygon(points1))
b = pya.Region(pya.Polygon(points2))

c = xor(a,b)
