# PIZZA_HOUSE_DB
Its my DBMS mini project which i did in college..basical containing MySQL Database.
-- phpMyAdmin SQL Dump
-- version 4.7.4
-- https://www.phpmyadmin.net/
--
-- Host: 127.0.0.1:3306
-- Generation Time: Nov 29, 2018 at 11:26 AM
-- Server version: 5.7.19
-- PHP Version: 5.6.31

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET AUTOCOMMIT = 0;
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `pizza house`
--

DELIMITER $$
--
-- Procedures
--
DROP PROCEDURE IF EXISTS `ECOUNT`$$
CREATE DEFINER=`root`@`localhost` PROCEDURE `ECOUNT` ()  select count(empname)
from employee$$

DELIMITER ;

-- --------------------------------------------------------

--
-- Table structure for table `bill`
--

DROP TABLE IF EXISTS `bill`;
CREATE TABLE IF NOT EXISTS `bill` (
  `crustname` varchar(20) DEFAULT NULL,
  `crustcost` int(10) DEFAULT NULL,
  `cheesename` varchar(20) DEFAULT NULL,
  `cheesecost` int(10) DEFAULT NULL,
  `saucename` varchar(20) DEFAULT NULL,
  `saucecost` int(10) DEFAULT NULL,
  `spicesname` varchar(200) DEFAULT NULL,
  `spicescost` int(10) DEFAULT NULL,
  `toppings` varchar(200) DEFAULT NULL,
  `toppingscost` int(10) DEFAULT NULL,
  `total` int(10) DEFAULT NULL,
  `cname` varchar(20) NOT NULL,
  `empid` varchar(10) DEFAULT NULL,
  PRIMARY KEY (`cname`)
) ENGINE=MyISAM AUTO_INCREMENT=6 DEFAULT CHARSET=latin1;

--
-- Dumping data for table `bill`
--

INSERT INTO `bill` (`crustname`, `crustcost`, `cheesename`, `cheesecost`, `saucename`, `saucecost`, `spicesname`, `spicescost`, `toppings`, `toppingscost`, `total`, `cname`, `empid`) VALUES
('handtossed', 150, 'mozarella', 50, 'pesto', 60, 'rosemary,onionflakes,', 45, 'mushroom,cheese,blackolives,spinach,', 100, 405, 'Abhi', '4321'),
('thincrust', 200, 'mozarella', 50, 'pesto', 60, 'rosemary,', 20, 'bacon,', 30, 360, 'jklk', '2345'),
('cheeseburst', 250, 'cheddar', 70, 'thaichili', 90, 'garlic,', 25, 'cheese,spinach,', 55, 490, 'harsh', '1234');

-- --------------------------------------------------------

--
-- Table structure for table `cheese`
--

DROP TABLE IF EXISTS `cheese`;
CREATE TABLE IF NOT EXISTS `cheese` (
  `name` varchar(20) NOT NULL,
  `cost` int(10) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `cheese`
--

INSERT INTO `cheese` (`name`, `cost`) VALUES
('mozarella', 50),
('provolone', 60),
('cheddar', 70),
('parmesan', 80);

-- --------------------------------------------------------

--
-- Table structure for table `crust`
--

DROP TABLE IF EXISTS `crust`;
CREATE TABLE IF NOT EXISTS `crust` (
  `name` varchar(20) NOT NULL,
  `cost` int(10) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `crust`
--

INSERT INTO `crust` (`name`, `cost`) VALUES
('handtossed', 150),
('thincrust', 200),
('cheeseburst', 250),
('panpizza', 100),
('classichandtossed', 200);

-- --------------------------------------------------------

--
-- Table structure for table `ctrigger`
--

DROP TABLE IF EXISTS `ctrigger`;
CREATE TABLE IF NOT EXISTS `ctrigger` (
  `exectime` datetime NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `ctrigger`
--

INSERT INTO `ctrigger` (`exectime`) VALUES
('2017-11-22 23:07:10'),
('2017-11-24 13:57:14'),
('2017-11-24 21:59:16'),
('2017-11-29 01:22:50'),
('2017-11-29 13:53:07'),
('2017-11-29 15:58:45'),
('2018-11-16 18:43:48'),
('2018-11-16 18:47:31'),
('2018-11-16 20:18:57'),
('2018-11-17 10:51:09'),
('2018-11-26 23:29:20');

-- --------------------------------------------------------

--
-- Table structure for table `customer`
--

DROP TABLE IF EXISTS `customer`;
CREATE TABLE IF NOT EXISTS `customer` (
  `name` varchar(50) NOT NULL,
  `number` varchar(50) NOT NULL,
  `empid` varchar(10) NOT NULL,
  `cnum` int(11) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`cnum`)
) ENGINE=MyISAM AUTO_INCREMENT=13 DEFAULT CHARSET=latin1;

--
-- Dumping data for table `customer`
--

INSERT INTO `customer` (`name`, `number`, `empid`, `cnum`) VALUES
('Abhi', '9008335504', '4321', 12),
('jklk', '897654', '2345', 11),
('harsh', '8748051242', '1234', 10);

--
-- Triggers `customer`
--
DROP TRIGGER IF EXISTS `custtrig`;
DELIMITER $$
CREATE TRIGGER `custtrig` BEFORE INSERT ON `customer` FOR EACH ROW insert into ctrigger
values(now())
$$
DELIMITER ;

-- --------------------------------------------------------

--
-- Table structure for table `employee`
--

DROP TABLE IF EXISTS `employee`;
CREATE TABLE IF NOT EXISTS `employee` (
  `empname` varchar(20) NOT NULL,
  `num` varchar(10) NOT NULL,
  `emailid` varchar(50) NOT NULL,
  `empid` varchar(10) NOT NULL,
  PRIMARY KEY (`empid`),
  UNIQUE KEY `empid` (`empid`)
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `employee`
--

INSERT INTO `employee` (`empname`, `num`, `emailid`, `empid`) VALUES
('kaleen', '6546379764', 'uytrdghdw', '4321'),
('kjkj', '98987', 'ghgf', '2345'),
('', '', '', ''),
('vivek', '987877', 'jhgyk', '1234');

-- --------------------------------------------------------

--
-- Table structure for table `sauce`
--

DROP TABLE IF EXISTS `sauce`;
CREATE TABLE IF NOT EXISTS `sauce` (
  `name` varchar(20) NOT NULL,
  `cost` int(10) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `sauce`
--

INSERT INTO `sauce` (`name`, `cost`) VALUES
('pesto', 60),
('hummus', 70),
('bbq', 90),
('salsa', 70),
('bechamel', 60),
('pumkin', 50),
('tapenade', 70),
('ricotta', 80),
('thaichili', 90),
('alfredo', 70);

-- --------------------------------------------------------

--
-- Table structure for table `spices`
--

DROP TABLE IF EXISTS `spices`;
CREATE TABLE IF NOT EXISTS `spices` (
  `name` varchar(20) NOT NULL,
  `cost` int(10) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `spices`
--

INSERT INTO `spices` (`name`, `cost`) VALUES
('oregano', 20),
('basil', 15),
('rosemary', 20),
('onionflakes', 25),
('chiliflakes', 15),
('garlic', 25);

-- --------------------------------------------------------

--
-- Table structure for table `toppings`
--

DROP TABLE IF EXISTS `toppings`;
CREATE TABLE IF NOT EXISTS `toppings` (
  `name` varchar(20) NOT NULL,
  `cost` int(10) NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1;

--
-- Dumping data for table `toppings`
--

INSERT INTO `toppings` (`name`, `cost`) VALUES
('pepperoni', 20),
('mushroom', 25),
('onion', 30),
('sausage', 25),
('bacon', 30),
('cheese', 30),
('blackolives', 20),
('greenpeppers', 20),
('pineapple', 25),
('spinach', 25);
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
