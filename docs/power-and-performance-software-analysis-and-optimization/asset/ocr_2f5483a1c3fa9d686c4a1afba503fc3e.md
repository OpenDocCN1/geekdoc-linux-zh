# 4.6 Step 5: Algorithmic improvement 67

Table 4.2 Git Values for sendemail.suppresscc and --suppress-cc (git-send-email - Linux Manual Page, 2014)
| Value | Effect |
|---|---|
| author | Avoid auto-ccing patch author |
| self | Avoid auto-ccing patch sender |
| cc | Avoid auto-ccing anyone mentioned in Cc lines of patch header |
| bodycc | Avoid auto-ccing anyone mentioned in Cc lines of patch description |
| sob | Avoid auto-ccing anyone mentioned in Signed-off-by lines |
| ccmd | Skip running --cc, which runs over each patch and generates additional CC.s. |
| body | sob + bodycc |
| all | disable auto-cc |

through sendemail.suppresscc configuration value. Table 4.2 contains the list of acceptable values. The author prefers to disable the auto-cc feature, and manually selects the recipients.

Using the --compose argument will open $GIT_EDITOR, in which a cover letter can be written, the first in the series, which can provide some background information for the patch series. During composing, the cover letter header can be set by filling in the line beginning with Subject; or with the --subject command-line argument. The emails can be sent as a reply to an existing email, by filling in the In-Reply-To: line during composing, or with the --in-reply-to command-line argument, with the corresponding Message-ID header.

When in doubt, the author recommends emailing the patches to yourself, and validating the results were exactly as expected, before sending them publicly.

# 4.6 STEP 5: ALGORITHMIC IMPROVEMENT

A common mistake after profiling is to jump directly into architectural tuning. The problem with skipping this phase is that the largest performances typically come from selecting a better algorithm, as opposed to tuning algorithm for a specific architecture. Remember, no matter how much time is spent tuning a bubblesort implementation, quicksort implementation will be faster.

When searching for algorithmic improvements, profile the CPU time to determine what operations occur frequently. Using this information, look for data structures that can perform the frequent operations cheaply and trade the costs over the less-frequent operations.

Coverage of specific algorithms and general algorithmic techniques, such as divide and conquer or dynamic programming, is out of the scope of this book, as