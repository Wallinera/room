import "./scss/style.scss";

import heroImg1Desktop from "../src/images/desktop-image-hero-1.jpg";
import heroImg2Desktop from "../src/images/desktop-image-hero-2.jpg";
import heroImg3Desktop from "../src/images/desktop-image-hero-3.jpg";
import heroImg1Mobile from "../src/images/mobile-image-hero-1.jpg";
import heroImg2Mobile from "../src/images/mobile-image-hero-2.jpg";
import heroImg3Mobile from "../src/images/mobile-image-hero-3.jpg";

import navBtnOpen from "../src/images/icon-hamburger.svg";
import navBtnClose from "../src/images/icon-close.svg";

import logo from "../src/images/logo.svg";
import leftIcon from "../src/images/icon-angle-left.svg";
import rightIcon from "../src/images/icon-angle-right.svg";
import arrow from "../src/images/icon-arrow.svg";
import aboutImgDark from "../src/images/image-about-dark.jpg";
import aboutImgLight from "../src/images/image-about-light.jpg";
import { useMediaQuery } from "react-responsive";
import { useState } from "react";

const heroData = [
{
heading: "Discover innovative ways to decorate",
text: ` We provide unmatched quality, comfort, and style for property owners
        across the country. Our experts combine form and function in bringing
        your vision to life. Create a room in your own style with our collection
        and make your property a reflection of you and what you love.`,

    imgMobile: heroImg1Mobile,
    imgDesktop: heroImg1Desktop,
    id: 1,

},
{
heading: "We are available all across the globe",
text: `With stores all over the world, it's easy for you to find furniture for
        your home or place of business. Locally, we're in most major cities
        throughout the country. Find the branch nearest you using our store
        locator. Any questions? Don't hesitate to contact us today.`,

    imgMobile: heroImg2Mobile,
    imgDesktop: heroImg2Desktop,

    id: 2,

},
{
heading: "Manufactured with the best materials",
text: ` Our modern furniture store provide a high level of quality. Our company
        has invested in advanced technology to ensure that every product is made
        as perfect and as consistent as possible. With three decades of
        experience in this industry, we understand what customers want for their
        home and office.`,
imgMobile: heroImg3Mobile,
imgDesktop: heroImg3Desktop,

    id: 3,

},
];

export default function App() {
const [selectedContentId, setSelectedContentId] = useState(1);
const selectedContent = heroData.find(
(content) => content.id === selectedContentId
);
const isLargeWidth = useMediaQuery({ minWidth: 900 });
const isDesktop = useMediaQuery({ minWidth: 1440 });

return (
<main className={`${isDesktop ? "desktop" : ""}`}>
<Navigation isDesktop={isDesktop} />
<Hero
heroImg={
isLargeWidth ? selectedContent.imgDesktop : selectedContent.imgMobile
}
setSelectedContentId={setSelectedContentId}
/>
<Shop selectedContent={selectedContent} />
<About />
</main>
);
}

function Navigation({ isDesktop }) {
const [isMobileNavOpen, setIsMobileNavOpen] = useState(false);

function onMenuBtnClick() {
document.body.style.overflow = !isMobileNavOpen ? "hidden" : "";

    setIsMobileNavOpen(!isMobileNavOpen);

}

return isDesktop ? (
<>
<nav className={`nav container`}>
<img src={logo} alt="Logo" className="nav__logo" tabIndex={0}></img>
<ul className="nav__links">
<li>
<a href="home" className="nav__link">
home
</a>
</li>
<li>
<a href="shop" className="nav__link">
shop
</a>
</li>
<li>
<a href="about" className="nav__link">
about
</a>
</li>
<li>
<a href="contact" className="nav__link">
contact
</a>
</li>
</ul>
</nav>
</>
) : (
<>
{isMobileNavOpen && <div className="overlay"></div>}

      <nav className={`nav container ${isMobileNavOpen ? "nav__open" : ""}`}>
        <img
          src={isMobileNavOpen ? navBtnClose : navBtnOpen}
          alt="menu button"
          className="nav__btn"
          onClick={onMenuBtnClick}
          onKeyDown={(e) => e.key === "Enter" && onMenuBtnClick()}
          tabIndex={0}
        ></img>

        {isMobileNavOpen ? (
          <ul className="nav__links">
            <li>
              <a href="-" className="nav__link">
                home
              </a>
            </li>
            <li>
              <a href="-" className="nav__link">
                shop
              </a>
            </li>
            <li>
              <a href="-" className="nav__link">
                about
              </a>
            </li>
            <li>
              <a href="-" className="nav__link">
                contact
              </a>
            </li>
          </ul>
        ) : (
          <img src={logo} alt="Logo" className="nav__logo"></img>
        )}
      </nav>
    </>

);
}

function Hero({ heroImg, setSelectedContentId }) {
function onClickRight() {
setSelectedContentId((id) => {
if (id < heroData.length) return id + 1;
else {
return 1;
}
});
}

function onClickLeft() {
setSelectedContentId((id) => {
if (id > 1) return id - 1;
else {
return heroData.length;
}
});
}

return (
<section className="hero">
<div className="hero__image-box">
<img src={heroImg} alt="hero content"></img>
</div>
<div className="hero__slider-btns">
<button onClick={onClickLeft}>
<img src={leftIcon} alt="left arrow"></img>
</button>
<button onClick={onClickRight}>
<img src={rightIcon} alt="right arrow"></img>
</button>
</div>
</section>
);
}

function Shop({ selectedContent }) {
return (
<section className="shop container">
<h1>{selectedContent.heading}</h1>
<p>{selectedContent.text}</p>
<a href="-">
SHOP NOW{" "}
<span>
<img src={arrow} alt="arrow pointing right" />
</span>
</a>
</section>
);
}

function About() {
return (
<section className="about">
<div className="about__img-box--dark">
<img src={aboutImgDark} alt="black colored furnitures" />
</div>
<div className="about__text-box container">
<h2>ABOUT OUR FURNITURE</h2>
<p>
Our multifunctional collection blends design and function to suit your
individual taste. Make each room unique, or pick a cohesive theme that
best express your interests and what inspires you. Find the furniture
pieces you need, from traditional to contemporary styles or anything
in between. Product specialists are available to help you create your
dream space.
</p>
</div>
<div className="about__img-box--light">
<img src={aboutImgLight} alt="black colored furnitures" />
</div>
</section>
);
}
