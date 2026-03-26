```{margin}

::::::{attention}
This page shows the graded assignment. 

Please open the assignment from [GitHub Classroom](https://classroom.github.com/a/Pu4INjCT) to work on it locally. If that link doesn't work (Repository Access Issue’), use this backup link: https://classroom.github.com/a/HCEwEvOj and create a team using your student ID.
::::::

```


# Graded assignment

```{custom_download_link} https://classroom.github.com/a/Pu4INjCT
:text: "GitHub Classroom repository"
:replace_default: "False"
```

```{custom_download_link} https://classroom.github.com/a/HCEwEvOj
:text: "GitHub Classroom repository backup, create a team using student ID"
:replace_default: "False"
```

When you've finished the workshops, you can start with the graded assignment You're going to solve the following structural model for displacements and internal forces using the matrix method:

```{figure} figures/graded_assignment_2026.svg
:class: sticky-margin
:align: center
:source: https://github.com/CIEM5000-TU-Delft/prepare_assignments/blob/solution_2026/student_files/graded_assignment_2026.vsdx

$EI_{\rm{towers}} = 4000 e^{-\cfrac{x \, \rm{[m]}}{828}} \, \rm{GNm^2}$, $EA_{\rm{towers}} = 13 e^{-\cfrac{x \, \rm{[m]}}{828}} \, \rm{GN}$, $EI_{\rm{bridge}} = 4000 \, \rm{GNm^2}$, $EA_{\rm{bridge}} = 13 \, \rm{GN}$
```

Which is an exotic mix of the Petronas Twin Towers and the Burj Khalifa.

You need to answer the following questions in your report:
1. Explain in words and math how you adapted/added code and/or procedures to solve this structure.
2. Make a table of all nodal displacement and show the displaced structure in a figure. Indicate how you identify nodes.
3. Show the normal force diagram of the structure in a figure.
4. Provide a figure of a free body diagram of the full structure in which you show all the forces working on the structure (including support reactions) with numerical values from your code. This specific figure can be hand drawn.
5. Provide a figure of a free body diagram of the indicated node with numerical values from your code. This specific figure can be hand drawn.

Then, add potential new implementations to your code in `./matrixmethod/`. Please note that `./matrixmethod/` doesn't include any solutions from the workshops. Add new `.py` or `.ipynb` files to solve the structure outside of `./matrixmethod/`. Add a report in `.pdf` or `.md` format in which you included answers and reasoning for all the questions. Make sure all the values/figures you use in the report are solved/created with your code. Except for question 4 and 5: the free-body-diagrams can be hand-drawn.

The deadline of the assignment is April 19th, 23:59, although you’re encouraged to finish it directly after completing workshop 2. Doing so allows you to split the workload evenly. Commit and push all your files to the provided GitHub Classroom repository to hand in your assignment. Your latest commit before the deadline in the `main` branch will be graded. Incomplete assignments will be graded with a 1. The full solution won't be provided. You can take the resit of this assignment in Q4. If you choose to do so, you can improve your first submission by resubmitting to the same repository. The deadline of the resit is June 21th, 23:59. For more information, see [](./course_information.md).
