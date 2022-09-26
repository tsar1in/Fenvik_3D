#include <iostream>
#include <vector>
template <class Iterator>
std::vector<std::vector<std::vector<int>>> CountPrefix(Iterator begin, Iterator end) {
  std::vector<int> vals(begin, end);
  std::vector<int> result(vals.size());
  if (result.empty()) {
    return result;
  }
  result[0] = vals[0];
  for (size_t i = 1; i < result.size(); i++) {
    result[i] = result[i - 1] + vals[i];
  }
  return result;
}
class SumRange {
  const std::vector<int> prefix_sum_;

 public:
  template <class Iterator>
  SumRange(Iterator begin, Iterator end) : prefix_sum_(CountPrefix(begin, end)) {
  }
  int64_t GetSum(size_t left, size_t right) const {
    if (left == 0) {
      return prefix_sum_[right];
    }
    return (prefix_sum_[right] - prefix_sum_[left - 1]);
  }
  size_t Size() const {
    return prefix_sum_.size();
  }
};
class FenvikTree {
  std::vector<std::vector<std::vector<int>>> ft_;
  int QuaryPref(int x, int y, int z) {
    int sum = 0;
    for (int i = x; i >= 0; i = (i & (i + 1)) - 1) {
      for (int j = y; j >= 0; j = (j & (j + 1)) - 1) {
        for (int k = z; k >= 0; k = (k & (k + 1)) - 1) {
          sum += ft_[i][j][k];
        }
      }
    }
    return sum;
  }

 public:
  explicit FenvikTree(int n) {
    ft_ = std::vector<std::vector<std::vector<int>>>(n);
    for (int k = 0; k < n; k++) {
      std::vector<std::vector<int>> tmp2(n);
      for (int j = 0; j < n; j++) {
        std::vector<int> tmp1(n);
        for (int i = 0; i < n; i++) {
          tmp1[i] = 0;
        }
        tmp2[j] = std::move(tmp1);
      }
      ft_[k] = std::move(tmp2);
    }
  }
  void Update(int x, int y, int z, int delta, int n) {
    for (int i = x; i < n; i = (i | (i + 1))) {
      for (int j = y; j < n; j = (j | (j + 1))) {
        for (int k = z; k < n; k = (k | (k + 1))) {
          ft_[i][j][k] += delta;
        }
      }
    }
  }
  int Quary(int x, int y, int z, int a, int b, int c) {
    return QuaryPref(a, b, c) - QuaryPref(x - 1, b, c) - QuaryPref(a, y - 1, c) + QuaryPref(x - 1, y - 1, c) -
           QuaryPref(a, b, z - 1) + QuaryPref(x - 1, b, z - 1) + QuaryPref(a, y - 1, z - 1) -
           QuaryPref(x - 1, y - 1, z - 1);
  }
};
int main() {
  int n;
  std::cin >> n;
  FenvikTree fs(n);
  while (true) {
    int prov;
    std::cin >> prov;
    if (prov == 1) {
      int x, y, z, delta;
      std::cin >> x >> y >> z >> delta;
      fs.Update(x, y, z, delta, n);
    }
    if (prov == 2) {
      int x, y, z, a, b, c;
      std::cin >> x >> y >> z >> a >> b >> c;
      std::cout << fs.Quary(x, y, z, a, b, c) << '\n';
    }
    if (prov == 3) {
      break;
    }
  }
  return 0;
}
