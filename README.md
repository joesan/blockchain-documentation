# blockchain-documentation

1. Two types of Software architectures exists - Centralized & Distributed
2. A Hybrid architecture is also possible Centrally Distributed architectures
3. Blockchain simply put is a tool to maintain Trust & Integrity in a peer-to-peer system
4. The challenge is to solve the Trust & Integrity in the worst of all situations

# The Blockchain challenge:

Here is a very simplistic view of what the actual miners do when mining for the Bitcoin, or rather to put it in mathematical terms, solving a puzzle - The puzzle is always to find the leading zeros in the resulting hash of a new block. The difficulty increased with the increasing number of leading zeros. For example., take a look at the following function written in Scala:

```
def sha256Hash(text: String) : String = String.format("%064x", new java.math.BigInteger(1, java.security.MessageDigest.getInstance("SHA-256").digest(text.getBytes("UTF-8"))))

def mineSomeShit(str: String, appender: String, difficulty: String): String = {
  val hashed = sha256Hash(str)
  println(hashed)
  if (hashed.take(difficulty.length).startsWith(difficulty))
   hashed
  else {
    val newString = str + appender
    (mineSomeShit(newString, appender + appender, difficulty))
  }
}
```
We will hash the String "Hello" and we will try to find a hash for the initial String "Hello" by adding a single character to "Hello" and we hash the resulting String and check if we have leading zeros that we need. So the call to solve this simplistic puzzle would be like this:

```
mineSomeShit("Hello", "1", "0")
```

See I'm setting the difficulty to single zero at the staring position of the resulting hash. If I find a match from the resulting hash, I return, but if not, I keep appending a 1 to the end of "Hello" and continue hashing the resulting new String. So a test run on my Mac would look this:

```
scala> mineSomeShit("Hello", "1", "0")
185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
948edbe7ede5aa7423476ae29dcd7d61e7711a071aea0d83698377effa896525
b11cd38a7f952ff52348c60fa6436ad041f4273a6ad43200b48747ff7aae8557
7c01a6b99ca7d331c85b2f6826cf5c6429613d617ced1a761e36298de903c1a5
3a914c051d4c6902b83b086ad982148a3213e0c3d3d29d46027b7d118f7fc599
9e77cc0f3906d514f79889ec8d49b94488f82178fb368fef286b26f3964aa077
8e8a20333f0fc59553b7a14a269206688508e653f5058e891711eba61cd5df17
3740a40fb9b1f71f6e69b8268335aaf451b077c0ffe0df94d46c229175f21a16
00c547c99864a134db0c95e459b885e34b5e3ecd70f134e574c593e7fb113ef3
```

So there we go! We found out the hash with a single leading zero - I solved this puzzle - I get a ShitCoin for my "Proof of Work". Let us now notch it up a little by setting the difficulty to finding 2 leading zeros in our resulting hash. A test run on my Mac is as below:

```
scala> loop("Hello", "1", "00")
185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
948edbe7ede5aa7423476ae29dcd7d61e7711a071aea0d83698377effa896525
b11cd38a7f952ff52348c60fa6436ad041f4273a6ad43200b48747ff7aae8557
7c01a6b99ca7d331c85b2f6826cf5c6429613d617ced1a761e36298de903c1a5
3a914c051d4c6902b83b086ad982148a3213e0c3d3d29d46027b7d118f7fc599
9e77cc0f3906d514f79889ec8d49b94488f82178fb368fef286b26f3964aa077
8e8a20333f0fc59553b7a14a269206688508e653f5058e891711eba61cd5df17
3740a40fb9b1f71f6e69b8268335aaf451b077c0ffe0df94d46c229175f21a16
00c547c99864a134db0c95e459b885e34b5e3ecd70f134e574c593e7fb113ef3
```

Ok! I get another ShitCoin - Glad that I can do this with my Mac! Let us notch it up even higher, this time around, the puzzle to solve is to find a hash with 3 leading zeros - Guess what, my Mac could not handle it, the JVM could not handle it! Here it is:

```
scala> loop("Hello", "1", "000") // I'm setting the difficulty to 3 leading zeros
185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969
948edbe7ede5aa7423476ae29dcd7d61e7711a071aea0d83698377effa896525
b11cd38a7f952ff52348c60fa6436ad041f4273a6ad43200b48747ff7aae8557
7c01a6b99ca7d331c85b2f6826cf5c6429613d617ced1a761e36298de903c1a5
3a914c051d4c6902b83b086ad982148a3213e0c3d3d29d46027b7d118f7fc599
9e77cc0f3906d514f79889ec8d49b94488f82178fb368fef286b26f3964aa077
8e8a20333f0fc59553b7a14a269206688508e653f5058e891711eba61cd5df17
3740a40fb9b1f71f6e69b8268335aaf451b077c0ffe0df94d46c229175f21a16
00c547c99864a134db0c95e459b885e34b5e3ecd70f134e574c593e7fb113ef3
e8cb73f4c56f07fe838d6ad0e4e659b79542d2db4b31895f2592986c71d7b235
fe6b9a3f791c9b5b8afc66b7d9975581e197575de38bb51e354dd3f537e58796
d94210fea07e7b95235e6a544338fa536751db1a941ee6659915e5ec8ae4c23f
1e09d7ac0a3f950d8a244ec50362a52c2d8b4f97b2d6703cf2af787f8836d82c
158727d24e0a72ed6a28b405232466eff0dcfafc8975be03a7fd5bcad9b6ea02
6f1ff66ba394c3c632a7e552846d9cdd14a57ad19d117a98272a4188ee805e9a
f56f777268162d1a149a69fa8aab070ee00e2215b3fea2123c016ea997185632
3b5b867d31ab7daf63c0a66eefd86a5cc0801b5044f2a21bd50f2e1cee671ec4
ace085f11c9d6a1bc36d4292a3c336d007df223e1adebdd65b6342c6a56d7b2a
ac4a86fcd4e85554a0dadd15d832bd97cd7d5d5e3bcdf3d843ee7a5867bd8c0a
e69f3899145b9e4c40802235183ea90f3cb21051fabd05dfe341166a2f4fdb4c
7c16a5ed55c6bda49bf5ef8cd72cfa45f24d4189ee987d36973642a1dbebaffe
62cd5b96ffad643ed45caa2020eb1bc9dd4719bb9743fda4049198d9f5ec6db6
93405577cf3300f06a36ef59aa0201b9aa391f6badb55871313ad9fc57d91aec
72d47bce4c4b90e3a2f9a5d29a2acb377aa5d18c4da1c611fd934764e7ba2c0d
java.lang.OutOfMemoryError: Java heap space
```

This is exactly what happens when mining BitCoins. You need computational power as the difficulty goes higher and higher with every batch of Blocks! 

Hopefully this journal should help somebody somewhere trying to understand the fundamental principle behind the inner machinary of how Blockchain and BitCoin fit together!

