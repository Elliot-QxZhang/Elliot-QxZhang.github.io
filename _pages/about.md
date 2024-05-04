---
permalink: /
title: ""
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I am a year-1 PhD Student at [The Hong Kong University of Science and Technology](https://hkust.edu.hk/zh-hans) under the supervision of [Prof. Xiaomeng Li](https://xmengli.github.io/). Previously, I was fortunate to work with [Prof. Yan Wang](https://cs.scu.edu.cn/info/1075/8235.htm) at Sichuan University as an undergraduate research intern.

My research lies at advancing medical image analysis with AI, with a recent focus on pathology image analysis.

News
------
<ul style="overflow:scroll; height:300px; width:100%; margin: 0 auto;">
    <li>[02/2024] One paper accepted by CVPR 2024! </li>
    <li>[08/2023] Join Prof. Xiaomeng Li’s lab at HKUST to pursue my Ph.D. degree. </li>
    <li>[07/2023] Glad to be an awardee of the HKUST RedBird PhD Recruitment Award. Thank you, HKUST!</li>
    <li>[06/2023] One paper accepted by MICCAI 2023!</li>
    <li>[11/2022] Accepting official offer letter from HKUST, preparing for PhD career in HKUST!</li>
    <li>[10/2022] Finished HK PolyU Research Summer Workshop and won the scholarship!</li>
    <li>[09/2022] Join HK PolyU Research Summer Workshop, moving to Hong Kong</li>
    <li>[06/2022] Glad to be an awardee of ZiLi-Zhi Dong First-class Scolarship. Thank you, Mr. Liu and Mr Zhu!</li>
    <li>[12/2021] Successfully finished CSITP on "RoboDentist" and got rated as Excellent</li>
    <li>[12/2021] Successfully finished CSITP on Knowledge Graph and got rated as Good</li>
    <li>[10/2021] Glad to receive the prize from NUS Summer Workshop (overall performance A Plus). Thank you, NUS! Moving back to Sichuan!</li>
    <li>[10/2021] Won the First Prize of NUS SoC Summer Workshop! Nice working with you, B. H and S. F!</li>
    <li>[06/2021] Moved to Singapore and joined NUS SoC Summer Workshop!</li>
    <li>[06/2021] Our Brain Disease Knowledge Graph got rated as provincial level College Student Innovative Training Project</li>
    <li>[06/2021] Our startup "RoboDentist" got rated as national level College Student Innovative Training Project</li>
    <li>[04/2020] Pass the qualification interview of NUS SoC Summer Workshop and Scholarship. Thank you, SCU!</li>
    <li>[12/2020] Successfully finished CSITP and got rated as Excellent</li>
    <li>[12/2020] One paper on vulnerability mining accepted by TrustCom 2021!</li>
    <li>[06/2020] Our startup "DeepVuler" was rated as national level College Student Innovative Training Project</li>
    <li>[09/2019] Changing major to Software Engineering!</li>
    <li>[02/2019] Glad to be awardee of outstanding student of Sichuan and Comprehensive First-class scholarship</li>
</ul>



Publications
------
  <div style="display: flex; align-items: center;">
    <img src="/images/2023-miccai-qzhang.png" alt="Image" style="width: 250px; height: auto; margin-right: 15px;">
    <p style="font-size: 14px;">
      <a href="https://arxiv.org/abs/2307.11989" style="color:#3498DB; font-weight: bold; font-size: 16px">Morphology-inspired Unsupervised Gland Segmentation via Selective Semantic Grouping</a><br>
      <strong>Qixiang Zhang</strong>, Yi Li and Xiaomeng Li <br>
      Medical Image Computing and Computer Assisted Intervention (<strong>MICCAI</strong>), 2023 
    </p>
  </div>



Site-wide configuration
------
The main configuration file for the site is in the base directory in [_config.yml](https://github.com/academicpages/academicpages.github.io/blob/master/_config.yml), which defines the content in the sidebars and other site-wide features. You will need to replace the default variables with ones about yourself and your site's github repository. The configuration file for the top menu is in [_data/navigation.yml](https://github.com/academicpages/academicpages.github.io/blob/master/_data/navigation.yml). For example, if you don't have a portfolio or blog posts, you can remove those items from that navigation.yml file to remove them from the header. 

Create content & metadata
------
For site content, there is one markdown file for each type of content, which are stored in directories like _publications, _talks, _posts, _teaching, or _pages. For example, each talk is a markdown file in the [_talks directory](https://github.com/academicpages/academicpages.github.io/tree/master/_talks). At the top of each markdown file is structured data in YAML about the talk, which the theme will parse to do lots of cool stuff. The same structured data about a talk is used to generate the list of talks on the [Talks page](https://academicpages.github.io/talks), each [individual page](https://academicpages.github.io/talks/2012-03-01-talk-1) for specific talks, the talks section for the [CV page](https://academicpages.github.io/cv), and the [map of places you've given a talk](https://academicpages.github.io/talkmap.html) (if you run this [python file](https://github.com/academicpages/academicpages.github.io/blob/master/talkmap.py) or [Jupyter notebook](https://github.com/academicpages/academicpages.github.io/blob/master/talkmap.ipynb), which creates the HTML for the map based on the contents of the _talks directory).

**Markdown generator**

I have also created [a set of Jupyter notebooks](https://github.com/academicpages/academicpages.github.io/tree/master/markdown_generator
) that converts a CSV containing structured data about talks or presentations into individual markdown files that will be properly formatted for the Academic Pages template. The sample CSVs in that directory are the ones I used to create my own personal website at stuartgeiger.com. My usual workflow is that I keep a spreadsheet of my publications and talks, then run the code in these notebooks to generate the markdown files, then commit and push them to the GitHub repository.

How to edit your site's GitHub repository
------
Many people use a git client to create files on their local computer and then push them to GitHub's servers. If you are not familiar with git, you can directly edit these configuration and markdown files directly in the github.com interface. Navigate to a file (like [this one](https://github.com/academicpages/academicpages.github.io/blob/master/_talks/2012-03-01-talk-1.md) and click the pencil icon in the top right of the content preview (to the right of the "Raw | Blame | History" buttons). You can delete a file by clicking the trashcan icon to the right of the pencil icon. You can also create new files or upload files by navigating to a directory and clicking the "Create new file" or "Upload files" buttons. 

Example: editing a markdown file for a talk
![Editing a markdown file for a talk](/images/editing-talk.png)

For more info
------
More info about configuring Academic Pages can be found in [the guide](https://academicpages.github.io/markdown/). The [guides for the Minimal Mistakes theme](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) (which this theme was forked from) might also be helpful.
