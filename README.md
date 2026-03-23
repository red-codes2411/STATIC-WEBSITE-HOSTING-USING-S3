#STATIC-WEBSITE-HOSTING-USING-S3
\documentclass[a4paper,12pt]{article}
\usepackage[margin=1in]{geometry}
\usepackage{titlesec}
\usepackage{enumitem}
\usepackage{hyperref}
\usepackage{fancyvrb}

\title{\textbf{STATIC-WEBSITE-HOSTING-USING-S3}}
\date{}

\begin{document}

\maketitle

\section*{🌐 AWS Static Portfolio Hosting (S3 + CloudFront)}

\section*{📌 Project Overview}
This project demonstrates how to deploy a personal portfolio website using AWS S3 for static hosting and CloudFront as a CDN layer.

The goal is to create a fast, scalable, and secure static website while understanding the fundamentals of AWS hosting and permissions.

\section*{🧩 Services Used}
\begin{itemize}
\item \textbf{Amazon S3} \\
Used to store and serve static files (HTML, CSS, JS) like a web server.

\item \textbf{AWS IAM (Identity and Access Management)} \\
Controls permissions and ensures only the required access is granted.

\item \textbf{Amazon CloudFront (CDN)} (Optional but Recommended) \\
Improves performance, enables HTTPS, and distributes content globally.
\end{itemize}

\section*{🚀 Features}
\begin{itemize}
\item Static website hosting using S3
\item Secure access configuration using IAM policies
\item Global content delivery using CloudFront
\item HTTPS support via CloudFront
\item Beginner-friendly AWS architecture
\end{itemize}

\section*{🛠️ Architecture}
\begin{verbatim}
User → CloudFront (CDN) → S3 Bucket (Static Website)
                    ↑
                  IAM (Access Control)
\end{verbatim}

\section*{📂 Project Structure}
\begin{verbatim}
/portfolio-project
│── index.html
│── style.css
│── script.js
│── assets/
│── README.md
\end{verbatim}

\section*{⚙️ Setup Guide}

\subsection*{🔹 Phase 1: Create S3 Bucket}
\begin{itemize}
\item Create a new S3 bucket
\item Disable "Block all public access"
\item Enable Static Website Hosting
\item Upload your portfolio files
\end{itemize}

\subsection*{🔹 Phase 2: Configure Bucket Policy}
Allow public read access using the following policy:

\begin{Verbatim}[fontsize=\small]
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::YOUR-BUCKET-NAME/*"]
    }
  ]
}
\end{Verbatim}

\subsection*{🔹 Phase 3: Access Website}
Use the S3 Website Endpoint URL to view your live site.

\subsection*{🔹 Phase 4: Important Concept}

\textbf{⚠️ Common Beginner Mistake}

Do NOT select the S3 bucket directly in CloudFront origin settings.

\textbf{Instead:}
\begin{itemize}
\item Copy and paste the S3 Website Endpoint URL manually
\end{itemize}

\textbf{❌ Wrong:} Selecting bucket from dropdown

\textbf{✅ Correct:}
\begin{verbatim}
http://your-bucket-name.s3-website-region.amazonaws.com
\end{verbatim}

\textbf{👉 Why this matters:}

The dropdown uses the REST API endpoint, which breaks static website routing (e.g., index.html, error pages).

\subsection*{🔹 Phase 5: CloudFront Distribution}
\begin{itemize}
\item Create a CloudFront distribution
\item Set origin as your S3 website endpoint
\item Enable Redirect HTTP → HTTPS
\item Wait for deployment (~15–20 minutes)
\end{itemize}

\subsection*{🔹 Phase 6: Access via CloudFront}
Use the generated CloudFront URL:

\begin{verbatim}
https://your-distribution-id.cloudfront.net
\end{verbatim}

\textbf{🎉 Your site is now:}
\begin{itemize}
\item Faster
\item Globally distributed
\item HTTPS enabled
\end{itemize}

\section*{⚠️ Important Note}
Whenever you update the existing code, you must upload it manually to the S3 bucket so that it overwrites the old version and reflects the latest changes.

This process can be automated using AWS Amplify or CI/CD pipelines.

\section*{🔮 Future Improvements}

\subsection*{🚀 AWS Amplify Integration}
\begin{itemize}
\item Automatic deployment from GitHub
\item Built-in CI/CD
\item Easy custom domain setup
\end{itemize}

\textbf{Benefits:}
\begin{itemize}
\item No manual uploads
\item Continuous updates on code push
\item Beginner-friendly deployment pipeline
\end{itemize}

\end{document}
