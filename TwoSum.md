//Java
// Step1/3
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] answer = new int[2];
        for (int i = 0; i < nums.length; i++) {
            for (int complement = i + 1; complement < nums.length; complement++) {
                if (target == nums[i] + nums[complement]) {
                    answer[0] = i;
                    answer[1] = complement;
                }
            }
        }
        return answer;
    }
}
// 所感
// 初見で何とかかけた。提出前に人のコードとレビューを読んでみると、complementという変数名を採用したほうが読みやすいと気づいたのでそこだけ修正した。
// 加えて、想定していない入力が来た時の返り値の処理を書いていないことにも気づかされた。Step2では想定外の入力への対処も考える。
// 次はHashMapを使って挑戦してみる。

## step2
ネスペの試験勉強などで長いこと手を付けられてなかったが、ようやく練習を再開できた。
以下練習中に思ったこと：
例えばnums = [3, 4, 7, 1]としたとき、3_1のように、numsの要素_その添え字をセットにする。それから、numsの要素を基準にソートして先頭と末尾を近づけながら目当ての組を探せばいいと考えて実装した。
想定外の入力への対処もしたかったが、ブランクが空きすぎて完全に忘れていた。
手作業でやるならどうするかを考えた結果の実装だが、今回の問題ではハッシュテーブルを使うという発想が納得のいく感じで出てこなかった。

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        record Pair(int num, int index) {};
        List<Pair> pair_list = new ArrayList<>();
        for (int i = 0; i < nums.length; i++) {
            pair_list.add(new Pair(nums[i], i));
        }
        pair_list.sort(Comparator.comparing(Pair::num));
        int head = 0;
        int tail = nums.length - 1;
        while (head < tail) {
            Pair p_head = pair_list.get(head);
            Pair p_tail = pair_list.get(tail);
            int pairsum = p_head.num() + p_tail.num();
            if (pairsum == target) {
                return new int[] {p_head.index(), p_tail.index()};
            } else if (pairsum < target) {
                head += 1;
            } else if (pairsum > target) {
                tail -= 1;
            }
        }
        return new int[] {};
    }
}

```
