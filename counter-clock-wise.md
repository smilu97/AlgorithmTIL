# Counter clockwise 함수로 선분간 관계 알아내기

임의의 2차원 벡터 a, b가 있을 때, 세 번째 축을 0으로 고정시켜 강제로 3차원 벡터로 만든 후에, cross곱\(외적\)의 크기를 구하면 그 값이 양수인지 음수인지를 보고 두 벡터의 각의 대소관계를 알 수 있다.

특히 Convex hull을 구하는 문제에서 쓰이기 때문에 중요하다.

## 두 선분의 충돌 감지

두 Line segment를 A, B라고 했을 때, A에 있는 두 점과, B에 있는 한 점을 골라\(2가지 경우가 있을 것이다\) 각각 a, b, c라고 했을 때 \(b-a\) 와 \(c-a\)의 CCW를 구한다. 나머지 하나의 경우에서도 똑같이 계산해서 두 값의 부호가 다르면 두 선분이 충돌한 것이다.

만약에 두 값의 부호가 같다면 A, B를 서로 바꾸고 다시 똑같이 시도해본다. 이 때도 여전히 두 값의 부호가 같다면 정말로 충돌하지 않는 것이고 여기서 부호가 달라도\(두 경우에서 하나라도 부호가 다르다면\) 두 선분은 충돌하는 것이다.

즉, 정리하자면 선분 A, B의 점 \(a, b, c, d\)가 있을 때

```cpp
struct vertex {
    int x, int y;
    vertex(int x=0, int y=0):x(x),y(y) {}
    vertex operator-(const vertex b) {
        return vertex(x-b.x, y-b.y);
    }
};
int ccw(vertex a, vertex b) { return a.x*b.y-a.y*b.x; }  // CCW를 계산
// 두 선분이 충돌하는지 판단(단, 평행하는 경우를 예외처리하지 않고있음)
bool isLineCollision(vertex a, vertex b, vertex c, vertex d) {
    return ccw(b-a, c-a)*ccw(b-a, d-a) < 0 || ccw(d-c, a-c)*ccw(d-c, b-c);
}
```

이 정도 코드로 정리할 수 있을 것 같다.

