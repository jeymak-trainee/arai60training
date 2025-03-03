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
