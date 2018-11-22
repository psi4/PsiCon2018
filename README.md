# PsiCon2018
Talks and documents from the Nov 2018 developers' meeting at GT

## Schedule
http://psicode.org/workshop_nov_2018.php

## Report

- ### Standards
  - [x] @fevangelista has made Psi4 safe for C++17 with psi4/psi4#1345.
  - [ ] The C++ standard for the whole of Psi shall be bumped from 11 to 14.
  - [ ] The target version for OpenMP shall be v3.1 to accomodate Clang on Mac for conda.
  - [ ] In a few more months, after it's settled in, we'll consider v5.0 and rewrite all the pragmas. For conda, this will likely require Intel-atop-Native (GCC/Clang/MSVC).

- ### Psi4 1.3
  - Min requirements for feature freeze:
    - [ ] c-optking --> py-optking
    - [ ] IR intensities
    - [ ] full Windows test suite
  - Aim for feature freeze (and possibly release if we're sprightly) in 2018.
  - Two ideas on Windows release. (1) A vanilla, unthreaded binary for Win is satisfactory for v1.3. (2) First impressions matter, so we need high-quality Win conda packages. This means Intel atop MSVC. License situation ok (infinitely renewable every 90 days). News from Intel on how we can run the build on Azure remote resources.


- ### ECP
  - [x] @andysim has plumbed @robashaw/libecpint into Psi's build system and called the library. Current status is probable memory error.
  - [ ] @andysim will continue libecpint integration, psi4/psi4#1340.
  - [ ] @loriab will prepare conda recipe for libecpint and distribute it on psi4 channel once mods are ready for upstream (check with @robashaw).
  - [ ] @loriab will add `qcel.periodictable.n_valence_electrons(shell=1)` to aid in computing frozen core.

- ### Forum
  - [ ] @JonathonMisiewicz will continue to monitor the forum and transfer unsolved issues to GH or PsiConfCall. He will be joined by @dsirianni, @zachglick, and @jeffschriber.
  - [ ] Post-it note pads available for prizes for next two years, so try to help out.

- ### IR
  - [x] @dsirianni will get correct structure for normco/dipole-deriv contraction.
  - [ ] @dsirianni will finish off Yamaguchi's IR notes and get a reference implementation into Psi4NumPy
  - [ ] @loriab will help hook it into Psi4 driver
  - [ ] @loriab will add Cfour IR intensities to the ref data in `tests/python/vibanalysis` so we can check results.

- ### TDDFT
  - [x] @dgasmith has reference implementation with PR code or outright diagonalization in place of Davidson, psi4/psi4#1349.
  - [ ] @amjames and @robertodr will continue working on stability and interface.
  - [ ] @CDSherrill will relinquish the secrets of Davidson solvers to python.

- ### Misc
  - [x] @amjames exported t2 amplitudes for read-only in PsiAPI mode in psi4/psi4#1344
  - [ ] @ssh2, @edeprince3, @fevangelista will prepare a wishlist for how Psi can aid strong correlation research.
  - [ ] @loriab will check new artwork into psi4media
  - [ ] @robertodr will continue re-wrapping libqt BLAS/LAPACK bindings to cblas to avoid fortran mangling issue. @loriab will grep Rob's account for the key script if given a likely string.
  - [ ] Timings will be run to demonstrate the performance of conda packages. We'll add badges and notes to assure people that binaries are high quality.
  - [ ] @loriab will add a `psi4-path-advisor --xcode` command for Mac.
  - [ ] @loriab will continue hunting O(N^2) arrays that we're not presently counting in dfhelper.
  - [ ] Though repetitive, we'll pull in @bozkaya's FNO PR.
  - [ ] Any in-house logo designs will be given license https://creativecommons.org/licenses/by-sa/4.0/

- ### Geometry Optimizers
  - [ ] @psi-rking will change "fragment" field into QCSchema.
  - [ ] @psi-rking will fix IRC.
  - [ ] @loriab will look closer at failing test cases of psi4/psi4#1335 and determine if they're psi4-caused or optking-caused.
  - [ ] @psi-rking will fix optking accordingly.
  - [ ] @psi-rking will modify geometry opt schema to match geomeTRIC and propose on QCSchema any absent fields it needs.
  - [ ] After optking interface is complete, @loriab will drop in geomeTRIC, too.


- ### Tensors
  - [ ] Based on @amjames investigations, he and @robertodr will trial xtensor (templated) in Psi4. Maybe xsimd, too.
  - [ ] If sucessful, we'll ask @hokru to redo his float work in xtensor, rather than copy Ugur's code which itself is a partial copy of libdpd.
  - [ ] Use hptt (high performance tensor transpose)

- ### Summary of User Survey Discussion from the Breakout Session:
  - Discussion _assumed_ the following two takeaways from the user survey, with minimal discussion about whether they were valid assumptions to make. Nothing else from the survey was accounted for.
     - We need to push people to use conda install
        - [ ] Perhaps people are manual installing rather than conda installing because they think Psi will be optimized for their machines that way? If so, just advertize how multiarch support when we compile the binaries means that’s a non-issue. Include benchmarks.
        - [ ] “Install me with conda” should perhaps replace “Fork me on GitHub” in the top-left corner of the Psi website.
     * We need to show how fast Psi is
        - [ ] For modules where Psi particularly efficient, report challenging calculations, tactfully
  - A few additional comments were made:
      - [ ] Update website design to signal modern software.
      - [ ] It may be advantageous to push Psi4Education harder, so people who use whatever program they’re most familiar with will be most familiar with Psi, due to their undergraduate days.
    
- ### Summary of User Forum Discussion from the Breakout Session:
  - Most SAPT questions appear to be from users who have little to no prior experience with computational chemistry. The SAPT documentation should be rewritten accordingly.
  - It would be ideal to get power users to answer more questions on the forum, so developers can stick to developing. This is, alas, not likely to happen.
  - It would be good to have graduate students keep an eye on the forum and report on how it’s doing at the monthly Psi conference calls, so the rest of the dev team can be aware of any changes in plans they may need to make. Volunteering were Jonathon, Dom, Zach, and Jeff.
  - It may be good to update the “coffee” message with a direct link to the forum.
  - For cases where a question requires specialized knowledge of certain Psi modules, it would be good for the developers to have a quick reference list of who to ping if the question has gone unanswered for a few days.
  - The StackOverflow accepted answer and upvote system works well. Accepted answer so we know when a question is answered. Both help users know which answers to read first.
    - The system we use, Discourse, has an endorsed plugin called “solved” for accepted answers.
    https://meta.discourse.org/t/discourse-solved-accepted-answer-plugin/30155
    - I don’t think the StackOverflow system works well for us in so far as it reorders answers. The current structure is thread-like, and each post may depend on the context of those prior in time. If we wanted to completely restructure the forums and have a comment system, sure. Otherwise, no. I think the like button will serve our purposes adequately here.
    
- ### Multilevel Distributed Sow/Reap
  - [x] @dgasmith prototyped pydantic SingleResult and nbody class that works!
  - [x] @loriab did a crude separation of cbs into plan/compute/consolidate functions.
  - [x] @alenaizan further developed nbody compute classe and elst embedding.
  - [ ] @loriab will help @alenaizan move elst embedding from kwarg to C option.
  - [ ] @loriab will adapt cbs plan/compute/consolidate to regen storage arrays, pull from json instead of P::e.globals, and tweak old dict fields into json cbsrec structure.
  - [ ] @jturney will help @JonathonMisiewicz do the same for findif
  - [ ] @dgasmith will write a planning fn to accomodate multilevel s/r in place of recursive driver. All pushing to psi4/psi4#1351.

- ### Reconcile molparse with QCArchive
  - [ ] @loriab will temporarily put aside list provenance and adjust molparse, qcdb, psi4 provenance writing (in various stages of implementation and PR) to outright, not list, provenance. Connectivity will be added to qcdb/psi4 `Molecule`s as a pass-through field.
  - [x] Community has decided molssi/qcschema#55 such that fragment order in a schema must be preserved by all consuming software and different fragment order constitutes a different molecule. In contrast, connectivity info is unordered.
  - [ ] @loriab will adapt molparse to handle non-contiguous fragments -- the last area in which molparse is less capable than QCSchema topology.
  - [ ] @loriab will add a pruning function so only geom/elem/molecular_charge/molecular_multiplicity are stored if all other fields are default.
  - [ ] When it won't cause disruption across three repos, fields will be renamed, e.g., elem --> symbols and geom --> geometry.
  - [ ] QCArchive Team will replace internal molecule with `qcel.molparse`.

- ### PsiCon2019
  - may be renamed by host
  - early November 2019 at Emory, hosted by @fevangelista.
